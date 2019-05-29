# Posibles Errores http code > 400 en la respuesta del Silent Charge

| HTTP code| Respuesta del servicio                   | Razón                       | Reintentable?                   |
| -------- | ---------------------------------------- | ----------------------------|-------------------------------- |
|400 | **code**: INVALID_MODEL, **message**: the requested model has invalid properties| Se envió algún parámetro inválido | **Sí**, corrigiendo los parámetros enviados en request a silent|
|401 | **code**: InvalidCredentials, **message**: No authorization token was found| No se envió **bearer de acceso** generado con SSO | **Sí**, enviando el bearer|
|401 | **code**: InvalidCredentials, **message**: caused by TokenExpiredError: jwt expired| Bearer generado con SSO expiró | **Sí**, generando un nuevo bearer y enviandolo en el silent|
|401 | **code**: InvalidCredentials, **message**: caused by JsonWebTokenError: jwt malformed| Bearer enviado no tiene formato correcto | **Sí**, generando un nuevo bearer y enviandolo en el silent|
|404 | **error_code**: DOCUMENT_NOT_FOUND, **error_description**: The document you requested is not found| | |
| 500  |**error_code**: ERROR_GETTING_PAYMENT_BY_ID, **error_description**: Exception has ocurred trying to get the payment by his id| Se incluyó un id de pago inválido en la url que llama al silent | **Sí**, modificando la url con el id correcto |
| 500  |**error_code**: ERROR_WAITING_FOR_PROMISES_TO_RESOLVE, **error_description**: Exception has ocurred waiting for all promises to resolve when trying to approve payments| Un proceso interno de búsqueda falló | **Sí** |
| 500 | **error_code**: REQUEST_ERROR, **error_description**: Exception has ocurred when trying tokenize the credit card in cybersource|
| 500 | **error_code**: GATEWAY_DATA_DONT_EXISTS, **error_description**: Exception ocurred when trying to read the cybersource response: reply message from cybersource is empty| Históricamente, este error ha ocurrido cuando la intención de pago lleva el nombre del producto con el caracter "&" y Cybersource rechaza. | Siempre y cuando se modifique el documento en base de datos |
| 500 | **error_code**: CYBERSOURCE_MISSING_REPLY, **error_description**: The response in cybersource has some invalid values| La respuesta de Cybersource tuvo un formato inválido | Se deberá revisar operativamente |
| 500 | **error_code**: DATABASE_ERROR_PAYMENT_UPDATE, **error_description**: Database error has ocurred when trying to update a payment document| Hubo un error al intentar actualizar el documento en la base de datos| **No**, se deber revisar el caso |
|502 | **error_code**: Bad Gateway| Problemas para llegar a nuestro servicio | Cuando se restablezca |
|503 | **error_code**: Service Temporarily unavailable, **error_description**: Service unavailable | Servicio indisponible | Cuando haya un restablecimiento |
|503 | **error_code**: Service Temporarily unavailable, **error_description**: name resolution failed | Servicio indisponible | Cuando haya un restablecimiento del servicio |
