¡De una! Acá tenés un **plan paso a paso** para un MVP 100% funcional con **n8n + WhatsApp Cloud API + AWS (Textract, S3, DynamoDB)**, sin dashboard web ni Next.js.

---

# 0) Qué va a poder hacer el MVP

- Crear un **grupo** (p. ej., “Asado-Vie”) y sumar amigos.
    
- Enviar por WhatsApp (1-a-1) la **foto del ticket**.
    
- Hacer **OCR** del ticket con **AWS Textract (AnalyzeExpense)** y sacar total/ítems.
    
- **Dividir** el gasto (por defecto, en partes iguales).
    
- Mostrar **estado** y **quién debe cuánto** (por WhatsApp).
    
- Marcar **pagos confirmados** por botón/aprobación desde WhatsApp.
    

> n8n tiene nodo nativo para WhatsApp Business Cloud (enviar mensajes, descargar media, esperar respuesta) y para AWS Textract. Y hay **WhatsApp Trigger** para recibir mensajes entrantes. ([n8n Docs](https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.whatsapp/ "WhatsApp Business Cloud node documentation | n8n Docs"))

---

# 1) Infra en AWS (mínimo)

1. **n8n**: montalo donde prefieras en AWS (simple: **Lightsail** o una **EC2** con Docker). Configurá URL pública y HTTPS (necesario para webhooks).
    
    - Variables típicas: `N8N_HOST`, `N8N_PORT`, `WEBHOOK_URL`.
        
2. **S3**: bucket `recibos-<tu-proyecto>` para guardar las fotos de tickets.
    
3. **DynamoDB** (una tabla **single-table**):
    
    - **PK** (string), **SK** (string), GSI opcional por teléfono.
        
    - **Entidades** sugeridas:
        
        - Grupo: `PK=GROUP#<code>`, `SK=METADATA` → nombre, admin, createdAt
            
        - Miembro: `PK=GROUP#<code>`, `SK=MEMBER#<phone>` → alias, joinedAt
            
        - Estado usuario: `PK=USER#<phone>`, `SK=STATE` → `awaiting="ticket"|null`, `groupCode`
            
        - Cuenta: `PK=GROUP#<code>`, `SK=BILL#<id>` → payer, s3Key, total, currency, split, createdAt
            
4. **Permisos/IAM** para n8n (rol o usuario):
    
    - `s3:PutObject/GetObject` en el bucket.
        
    - `textract:AnalyzeExpense` en la región del bucket. (Textract soporta **AnalyzeExpense** con `Document.S3Object` y devuelve `SummaryFields` y `LineItemGroups`). ([AWS Documentation](https://docs.aws.amazon.com/textract/latest/dg/API_AnalyzeExpense.html "AnalyzeExpense - Amazon Textract"))
        
    - `dynamodb:PutItem/Query/UpdateItem`.
        

---

# 2) WhatsApp Cloud API (Meta)

1. Creá App en **Meta for Developers**, asociá tu **WABA** y número, generá **token**, obtené **Phone Number ID**.
    
2. En n8n, creá **credencial de WhatsApp Business Cloud**.
    
3. Poné un **webhook** hacia n8n (usando el **WhatsApp Trigger**). Este trigger recibe eventos de mensajes entrantes. ([n8n Docs](https://docs.n8n.io/integrations/builtin/trigger-nodes/n8n-nodes-base.whatsapptrigger/ "WhatsApp Trigger node documentation | n8n Docs"))
    
4. (Opcional) Registrá **templates** para notificaciones y **mensajes interactivos** (botones/listas). Meta documenta “**interactive messages**”. ([Postman](https://www.postman.com/meta/whatsapp-business-platform/folder/iyy9vwt/sending-interactive-messages?utm_source=chatgpt.com "Sending Interactive Messages | WhatsApp Business Platform"))
    
5. Para **media**: cuando recibís una imagen, te llega un **media id** que luego descargás (n8n tiene operación **Media → Download**). ([Desarrolladores de Facebook](https://developers.facebook.com/docs/whatsapp/cloud-api/reference/media/?utm_source=chatgpt.com "Media - WhatsApp Cloud API - Meta for Developers"), [n8n Docs](https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.whatsapp/ "WhatsApp Business Cloud node documentation | n8n Docs"))
    

---

# 3) Workflows en n8n

## WF-A: “Entrantes de WhatsApp → Orquestación”

**Dispara:** `WhatsApp Trigger` (mensaje entrante). ([n8n Docs](https://docs.n8n.io/integrations/builtin/trigger-nodes/n8n-nodes-base.whatsapptrigger/ "WhatsApp Trigger node documentation | n8n Docs"))

**Ramas principales (Switch por texto/tipo):**

1. **Crear grupo**
    
    - Texto: `crear grupo <nombre>`
        
    - **Code node**: genera `groupCode` (ej. 6 letras).
        
    - **DynamoDB (Put)**: Grupo + Miembro admin.
        
    - **WhatsApp (Send)**: “Listo. Código: _ABC123_. Invitá a tus amigos a mandar: `unirme ABC123`”.
        
    - (Podés usar **Send and Wait for Response** si querés confirmación). ([n8n Docs](https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.whatsapp/ "WhatsApp Business Cloud node documentation | n8n Docs"))
        
2. **Unirse a grupo**
    
    - Texto: `unirme <code>`
        
    - **DynamoDB (Put)**: `MEMBER#<phone>` en el grupo.
        
    - **WhatsApp (Send)**: “Te uniste a . Comandos: `ticket`, `estado`, `pague 2500`”.
        
3. **Subir ticket**
    
    - Texto: `ticket`
        
    - **DynamoDB (Update)** estado de usuario → `awaiting="ticket"`, `groupCode=<code actual>`
        
    - **WhatsApp (Send)**: “Enviame ahora _la foto del ticket_.”
        
4. **Imagen recibida**
    
    - Condición: `message.type === "image"` y estado del usuario `awaiting="ticket"`.
        
    - **WhatsApp (Media → Download)**: descarga binaria de la foto. ([n8n Docs](https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.whatsapp/ "WhatsApp Business Cloud node documentation | n8n Docs"))
        
    - **S3 (Upload)**: guarda `s3://recibos-.../groupCode/billId.jpg`.
        
    - **AWS Textract (AnalyzeExpense)**: entrada `S3Object` → devuelve total, ítems, etc. ([n8n Docs](https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.awstextract/?utm_source=chatgpt.com "AWS Textract node documentation"), [AWS Documentation](https://docs.aws.amazon.com/textract/latest/dg/API_AnalyzeExpense.html "AnalyzeExpense - Amazon Textract"))
        
    - **Code node (parseo)**:
        
        - Lee `SummaryFields` → `TOTAL`, `SUBTOTAL`, `TAX`, `DATE`.
            
        - Lee `LineItemGroups` → descripción + monto por ítem. ([AWS Documentation](https://docs.aws.amazon.com/textract/latest/dg/invoices-receipts.html?utm_source=chatgpt.com "Analyzing Invoices and Receipts - Amazon Textract"))
            
    - **DynamoDB (Put)**: guarda la **cuenta** `BILL#<id>` con los datos crudos de Textract.
        
    - **Cálculo del split (igualitario MVP)**:
        
        - Obtiene miembros del grupo.
            
        - `montoPorCabeza = total / cantMiembros` (redondeo al centavo).
            
    - **DynamoDB (Update)**: guarda split calculado (por miembro).
        
    - **WhatsApp (Send)** al _uploader_: “Total $X. ¿Divido _en partes iguales_ entre N? (Sí/No)”.
        
        - Usá `Send and Wait for Response` con **Approval** (botón “Sí, dividir”). ([n8n Docs](https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.whatsapp/ "WhatsApp Business Cloud node documentation | n8n Docs"))
            
5. **Confirmada la división**
    
    - **WhatsApp (Send)** a **cada miembro** (1-a-1):
        
        - Mensaje interactivo: “Te toca $Y. ¿Confirmás?” con botón **Confirmar**. (Los **interactive messages** y “esperar respuesta” suben mucho la tasa de respuesta). ([Postman](https://www.postman.com/meta/whatsapp-business-platform/folder/iyy9vwt/sending-interactive-messages?utm_source=chatgpt.com "Sending Interactive Messages | WhatsApp Business Platform"))
            
    - **DynamoDB (Update)**: marca `due[phone] = Y`, `status="pending"`.
        
6. **Pagos**
    
    - Texto: `pague <monto>` o botón de **Aprobación** (si preferís sólo “Confirmar pagado”).
        
    - **DynamoDB (Update)**: `paid[phone] += monto`, `status="paid"` si cubrió su parte.
        
    - **WhatsApp (Send)** (opcional): “¡Gracias! Queda saldo $Z”.
        
7. **Estado**
    
    - Texto: `estado`
        
    - **Code node**: calcula dinámicamente: pagado/pendiente por miembro.
        
    - **WhatsApp (Send)**: tabla simple en texto:
        
        ```
        Grupo Asado-Vie
        • +54 9 11 3... → $2.500 pendiente
        • +54 9 11 6... → $0 (listo)
        Total: $10.000 | Pendiente: $2.500
        ```
        

> Para recibir **media id** y descargar imágenes usás el recurso de **Media**; WhatsApp Cloud lo soporta y n8n tiene la operación **Media→Download**. ([Desarrolladores de Facebook](https://developers.facebook.com/docs/whatsapp/cloud-api/reference/media/?utm_source=chatgpt.com "Media - WhatsApp Cloud API - Meta for Developers"), [n8n Docs](https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.whatsapp/ "WhatsApp Business Cloud node documentation | n8n Docs"))

---

## WF-B: “Recordatorios”

**Dispara:** `Schedule Trigger` (p. ej., cada tarde) o comando `recordatorio`.

- **DynamoDB (Query)**: miembros con `status="pending"`.
    
- **WhatsApp (Send Template o texto)**: “Te queda $Y del grupo ”.
    
- (Podés usar **templates** si querés mensajería proactiva fuera de ventanas de servicio). ([Postman](https://www.postman.com/meta/whatsapp-business-platform/folder/iyy9vwt/sending-interactive-messages?utm_source=chatgpt.com "Sending Interactive Messages | WhatsApp Business Platform"))
    

---

# 4) Mensajes / Comandos (MVP)

- `crear grupo <nombre>` — crea grupo y da **código**.
    
- `unirme <código>` — se suma al grupo.
    
- `ticket` — pone al usuario en modo “esperando foto”.
    
- (Foto del ticket) — dispara OCR + split.
    
- `estado` — muestra resumen.
    
- `pague <monto>` — registra pago (o botón “Confirmar pagado”).
    

> Si querés **asignación por ítems** en vez de partes iguales, se agrega luego una ronda de **listas interactivas** para que cada miembro “reclame” ítems; la Cloud API soporta **list/quick replies** y n8n puede “**Send and Wait for Response**”. ([Postman](https://www.postman.com/meta/whatsapp-business-platform/folder/iyy9vwt/sending-interactive-messages?utm_source=chatgpt.com "Sending Interactive Messages | WhatsApp Business Platform"), [n8n Docs](https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.whatsapp/ "WhatsApp Business Cloud node documentation | n8n Docs"))

---

# 5) Consideraciones clave

- **Tamaño/formatos**: Textract (sync) acepta **JPEG/PNG/PDF/TIFF** hasta 10 MB por página; si vas a PDFs largos, usá modo async. ([AWS Documentation](https://docs.aws.amazon.com/textract/latest/dg/API_AnalyzeExpense.html "AnalyzeExpense - Amazon Textract"))
    
- **Región**: el bucket S3 y Textract deben estar en la **misma región**. ([AWS Documentation](https://docs.aws.amazon.com/textract/latest/dg/API_AnalyzeExpense.html "AnalyzeExpense - Amazon Textract"))
    
- **Privacidad**: guardá sólo lo necesario (campos del ticket + totales).
    
- **Costos**: Textract cobra por **página** (varía por región y API). Revisá “Textract Pricing”. ([Amazon Web Services, Inc.](https://aws.amazon.com/textract/pricing/?utm_source=chatgpt.com "Textract Pricing Page"))
    

---

# 6) Siguientes mejoras (cuando el MVP ya funcione)

- **Revisión humana** si la confianza de Textract en `TOTAL` es baja (pedir confirmación al uploader).
    
- **Propinas/desc/IVA**: leer `SummaryFields` y mostrarlos en la confirmación. ([AWS Documentation](https://docs.aws.amazon.com/textract/latest/dg/invoices-receipts.html?utm_source=chatgpt.com "Analyzing Invoices and Receipts - Amazon Textract"))
    
- **Pagos**: enviar **link de pago** (ej. Mercado Pago) y marcar pagado al recibir webhook.
    
- **Exportar**: generar CSV de cada cuenta (n8n → “GDrive/Email”).
    

---

## ¿Querés que te lo deje “listo para importar” en n8n?

Te puedo armar los **2 workflows** (A y B) con:

- nodos ya encadenados,
    
- estructura de DynamoDB (single-table),
    
- mapeos para WhatsApp (Media Download / Send & Wait),
    
- y la llamada a **Textract AnalyzeExpense** con `S3Object`. ([n8n Docs](https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.whatsapp/ "WhatsApp Business Cloud node documentation | n8n Docs"), [AWS Documentation](https://docs.aws.amazon.com/textract/latest/dg/API_AnalyzeExpense.html "AnalyzeExpense - Amazon Textract"))
    

Decime si preferís **Lightsail** para n8n (es lo más simple) y en qué **región** de AWS estás trabajando, así lo ajusto.