# Proyecto: Marketing personalizado por correo electrónico para Agencia de Viajes

## Resumen
Este proyecto permite generar, de manera automatizada utilizando inteligencia artificial, correos electrónicos de marketing para promocionar ofertas de viajes en base a las características e intereses de los clientes.

## Introducción
### Presentación del problema a abordar
El problema que se pretende abordar en el presente Proyecto es el de optimizar y automatizar las campañas de marketing personalizado a través de correo electrónico para una agencia de viajes pequeña. Actualmente, el proceso se realiza en forma manual apuntando a los clientes en general y no como un cliente individual con sus propios intereses y preferencias. Esta modalidad no solo consume mucho tiempo y es ineficiente para la agencia de viajes sino que, además, hace que los clientes reciban ofertas irrelevantes disminuyendo la tasa de conversión y perdiendo la oportunidad de vender paquetes que sí satisfagan las necesidades específicas del cliente.

### Desarrollo de la propuesta de solución
Se propone utilizar inteligencia artificial para generar correos electrónicos personalizados para los distintos segmentos de clientes (por ejemplo, viajeros aventureros, amantes del lujo, familieros, viajeros de negocios, viajeros gasoleros, etc.). Además, se propone utilizar inteligencia artificial para generar imágenes que acompañen a cada correo y que sean atractivas para el cliente.\
Para la generación de correos electrónicos de marketing personalizado, se le indicará al modelo el segmento de clientes al que va dirigida la oferta y detalles de la misma (tipo de destino, descuento a ofrecer, características de la oferta, tono del correo electrónico, etc.). Un prompt possible para esta tarea sería: “Genera un correo electrónico de marketing para un viajero ‘segmento’ interesado en ‘tipo de destino’. Ofrecele un descuento del ‘porcentaje de descuento’ en un ‘tipo de alojamiento’ en ‘destino’. El tono debe ser ‘tono1’ y ‘tono2’”. Ejemplo: “Genera un correo electrónico de marketing para un viajero de lujo interesado en playas paradisíacas. Ofrecele un descuento del 20 % en un resort all-inclusive en Cancún. El tono debe ser elegante y exclusivo”. En este caso se usará un modelo de “texto-a-texto”.\
Para la generación de las imágenes, se aplicará un primer paso usando un modelo de texto a texto para generar prompts más precisos que los redactados por humanos para la generación de imágenes basadas en el segmento del cliente y en el destino ofertado. Luego, en un segundo paso, se aplicará el prompt generado en un modelo "texto-a-imagen" para generar la imagen en sí. Un prompt posible para la generación del prompt sería: "Genera un prompt para crear una imagen fotorrealista a ser usada en un correo electrónico de marketing para un viajero ‘segmento’ al que nuestra agencia de viajes le está ofreciendo un descuento para un viaje a ‘destino’". Ejemplo: "Genera un prompt para crear una imagen fotorrealista a ser usada en un correo electrónico de marketing para un viajero de lujo al que nuestra agencia de viajes le está ofreciendo un descuento para un viaje a Cancún".\
Para identificar las características de las ofertas que podrían resultar atractivas a los clientes, se analizó un set de datos de viajes conteniendo información sobre fechas del viaje, duración, destino, nombre, edad, género y nacionalidad del/la pasajero/a, tipo de alojamiento y transporte, y costo de alojamiento y transporte.

### Justificación de la viabilidad del proyecto
Se considera que la implementación del proyecto se puede lograr en pocas semanas utilizando las herramientas disponibles en el mercado (como la API de OpenAI’s) y sin necesidad de entrenar un modelo.\
En caso de usar la API de Open AI’s y los modelos GPT-4o-mini y DALL-E-3, estas tienen un costo aunque no es muy elevado:\
- El input para generar el correo es de ~ 120 tokens (~80 tokens el prompt y ~40 tokens la descrpción del sistema), por lo que su costo es de 120 tokens * 0.15 USD/1M = USD 0.000018
- El output del prompt usado para generar el correo está limitado a 200 tokens como máximo, entonces el costo es 200 tokens * 0.60 USD/1M = USD 0.00012
- El input para generar el prompt es de ~ 120 tokens (~80 tokens el prompt y ~40 tokens la descrpción del sistema), por lo que su costo es de 120 tokens * 0.15 USD/1M = USD 0.000018
- El output del prompt usado para generar el correo está limitado a 200 tokens como máximo, entonces el costo es 200 tokens * 0.60 USD/1M = USD 0.00012
- La generación de imágenes de 1024x1024 pix (como las usadas en este proyecto) de calidad estándard usando DALL-E-3 tiene un costo de USD 0.04 por imágen
- Costo total de generar cada correo electrónico (incluyendo la imagen): USD 0.000018 + USD 0.00012 + USD 0.000018 + USD 0.00012 + USD 0.04 = USD 0.040276\
Entonces, esto significaría un costo de 40.27 USD para generar 1.000 correos electrónicos.\
En cuanto al costo de utilizar PandasAI para analizar el set de datos, este depende del tamaño del set de datos. A modo de ejemplo, un set de datos como el analizado con 150 registros ocupa menos de 10.000 tokens y su análisis tuvo un costo < 0.01 USD. Dado que este tipo de análisis se haría unas pocas veces para cada campaña de marketing, se considera que su costo no tendría mayor impacto en el proyecto.\
Además, habría que considerar el costo de una plataforma de email marketing (como Mailchimp). Mailchimp tiene un plan estándar de 500 contactos y 6.000 mails por mes de 20 USD/mes. Si se generaran y se enviaran 6.000 correos electrónicos por mes, el costo de la API de Open AI’s y de Mailchimp sería de 0.06 USD/correo electrónico. Este costo no es elevado, por lo que se considera que el proyecto es técnica y económicamente viable.

## Objetivos
- Generar correos electrónicos de marketing personalizado en base a las características e intereses del cliente
- Generar imágenes relevantes para aumentar el atractivo de dichos correos

## Metodología
1. Análisis de set de datos de viajes para identificar los destinos más populares y los tipos de alojamientos preferidos en esos destinos.
2. Generación del correo electrónico de marketing personalizado en base a los parámetros ingresados (nombre del cliente, segmento, tipo de destino de interés, porcentaje de descuento ofrecido, tipo de alojamiento ofrecido, destino ofertado, y tono del correo electrónico).
3. Generación del prompt para generar una imagen a incluir en el correo electrónico de marketing en base al segmento del cliente y al destino ofertado
4. Generación de la imagen para el correo electrónico de marketing usando el prompt generado en el punto 3
   
## Herramientas y tecnologías
- Excel (para traducir, limpiar y normalizar el set de datos)
- Colab
- Python
- PandasAI
- ChatGPT-4o mini
- DALL-E 3
En todos los prompts se utilizó la técnica de zero shoot prompting ya que el conocimiento previo del modelo permitió obtener respuestas satisfactorias a la vez que permitió optimizar los recursos.

## Implementación
El código para implementar la solución propuesta se encuentra en el siguiente [link](https://colab.research.google.com/drive/18Z7C9NkEcMm7R17minr08iqMq9frEhP2?usp=sharing)

## Resultados
La implementación brinda resultados muy buenos, considerando la facilidad y rapidez de la implementación y su bajo costo. Los correos electrónicos generados son, en general. satisfactorios aunque, a veces, el modelo agrega detalles que no fueron incluídos en el prompt (como, por ejemplo, un código de descuento). En el caso de las imágenes, los resultados son menos satisfactorios, ya que si bien son fotorrealistas, mantienen un aspecto artificial siendo notorio que no representan lugares reales.

## Conclusiones
Considero que se han logrado los objetivos del proyecto ya que se han generado de manera automatizada correos electrónicos de marketing personalizado en base a las características e intereses del cliente junto con una imagen relevante. Sin embargo, en el caso del texto de los correos electrónicos sería aconsejable realizar un control manual sobre los mismos para evitar que contengan información adicional errónea y mejorar aún más el prompt. Respecto a las imágenes, el hecho que se note que son generadas artificialmente, puede ser beneficioso en el sentido que no implican una obligación contractual aunque seguramente son mucho menos atractivas que las fotos de lugares reales.

## Referencias
El set de datos usados para determinar las características de las ofertas a promocionar, fue descarado de [Kaggle](https://www.kaggle.com/datasets/rkiattisak/traveler-trip-data). Según el autor, los datos fueron generados con LLMs. Para su uso en este proyecto, los datos fueron traducidos al español, limpiados y normalizados usando Excel.
