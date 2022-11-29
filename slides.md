---
# try also 'default' to start simple
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://www.pantechelearning.com/wp-content/uploads/2021/02/ML-PRO_Banner-2.jpg.png
# apply any windi css classes to the current slide
class: 'text-center'
# https://sli.dev/custom/highlighters.html
highlighter: shiki
# show line numbers in code blocks
lineNumbers: false
# some information about the slides, markdown enabled
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
# persist drawings in exports and build
drawings:
  persist: false
# use UnoCSS
css: unocss
---

## Instituto Tecnológico Gustavo A. Madero

# CHATBOT

Realizado por
<br>Obrajero Arguelles Mariana Abigail 
<br>Ruiz Bernal Eddy V.


---

# Introducción

- La **atención al usuario** es importante en cualquier tipo de institución pues esto depende de la satisfacción y necesidad que los usuarios tienen de sus servicios. 
<br>
- La **IA** (Inteligencia Artificial) es la técnica de programar una computadora para responder a los datos de la misma manera que lo hace un ser inteligente. Se puede considerar como una simulación de cómo un ser inteligente reacciona, procesa y entiende los datos.
<br>
- Un **chatbot** es un programa informático que simula y procesa conversaciones humanas, permitiendo así a los humanos
interactuar con dispositivos digitales como si se estuvieran comunicando con una persona real. 

<center>
<img border="rounded" src="https://scontent.fcvj4-1.fna.fbcdn.net/v/t1.15752-9/316415151_502644718505591_398748662092525401_n.jpg?_nc_cat=103&ccb=1-7&_nc_sid=ae9488&_nc_eui2=AeGU9vVcl_G_Hkzq1CH757dty7J8iLapmzLLsnyItqmbMmF8IyO_4nmLTs7sYKd42-2elL86WiP6fGRVlQfoyr78&_nc_ohc=NLTqNxUH6dsAX9XOM1_&_nc_ht=scontent.fcvj4-1.fna&oh=03_AdT8AXqaIBIJ5f-kItycHh297kGh269ZHlE1g9ijQH4ZGg&oe=63ABAE4B" />
</center>

<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 20%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
img {
  width:170px;
  height:180px;
}
</style>

---

# Proyecto
<br>

## Chatbot con data science

### Objetivos

|     |     |
| --- | --- |
| General| Desarrollar un chatbot utilizando la IA para la institución ITGAM en un periodo de tres meses, evaluando las respuestas y comparando la rápidez del servicio e información que se brinde podremos definir la eficiencia del chatbot. |
| Específicos | •	Analizar la eficiencia y rapidez del sistema de preguntas y respuestas del ITGAM. <br> •	Establecer la estructura de un chatbot así como conocer las partes que lo componen. <br> •	Organizar la información del ITGAM para después juntarla con el chatbot. <br> •	Categorizar el tipo de preguntas que se realicen en la plataforma del ITGAM. |

<!-- https://sli.dev/guide/animations.html#click-animations -->


<style>
h2 {
  background-color: #81F7F3;
  background-image: linear-gradient(45deg, #2E9AFE 10%, #81F7F3 20%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

---

# Marco Teórico
<div class="container-column">
<div class="container-cards">
  <div class="card_information">
  <div class="container">
    <h4><b>Algoritmos de aprendizaje automático</b></h4>
    <p>En un modelo de aprendizaje automático, el objetivo es establecer o detectar patrones que los usuarios puedan usar para hacer predicciones o clasificar información.</p>
  </div>
  
  <div class="container">
    <h4><b>Procesamiento del Lenguaje Natural</b></h4>
    <p>Campo de conocimiento de la Inteligencia Artificial que se ocupa de la investigar la manera de comunicar las máquinas con las personas mediante el uso de lenguas naturales, como el español, el inglés o el chino.</p>
  </div>

  <div class="container">
    <h4><b>Chatbot</b></h4>
    <p>Los chatbots pueden ser tan sencillos como programas rudimentarios que responden a consultas sencillas con una respuesta de una sola línea o tan sofisticados como los asistentes digitales que pueden aprender y evolucionar para ofrecer niveles de personalización cada vez mayores a medida que reúnen y procesan información.</p>
  </div>
</div>
</div>
</div>

---

# Desarrollo

Para desarrollar el chatbot nos apoyamos en algunas librerías:

```ts 
import json
from fastapi import FastAPI, Request
import httpx
import os

from google.cloud import dialogflow_v2 as dialogflow

app = FastAPI()

@app.post("/webhook")
async def webhook(resquest: Request):
    message = await resquest.json()
    chat_id = message["message"]["from"]["id"]
    message_recive = message["message"]["text"]

    text = "hola crack"
    url = "https://api.telegram.org/bot5537442272:AAFY-TpAkov4kzsrSMWyqx030BqCG-tMBpg/sendMessage"
```
---

    ```ts
    os.environ["GOOGLE_APPLICATION_CREDENTIALS"] = "ga.json"

    client = dialogflow.SessionsClient()
    session = client.session_path(project="alert-operation-339022", session="me")
    text_input = dialogflow.TextInput(text=message_recive, language_code="es")
    query_input = dialogflow.QueryInput(text=text_input)
    response = client.detect_intent(query_input=query_input, session=session)

    async with httpx.AsyncClient() as client:
        reponse = await client.post(
            url=url,
            json={"chat_id": chat_id, "text": response.query_result.fulfillment_text},
        )

    return message
---

# Creación del bot
<center>
<div>
Intents
<img id="img1" border="rounded" src="/img/bot1.jpg" /><br><img id="img2" border="rounded" src="/img/bot2.jpg" />
</div>
</center>

<style>
#img1{
  width:400px;
  height:150px;
}
#img2{
  width:220px;
  height:240px;
}
</style>

---

<center>
<div>
Respuestas
<img id="img3" border="rounded" src="/img/bot3.jpg" /><br>Generación del bot<img id="img4" border="rounded" src="/img/b4.jpg" />
</div>
</center>

<style>
#img3{
  width:490px;
  height:150px;
}
#img4{
  width:540px;
  height:230px;
}
</style>

---

<center>
<div>
Telegram Token
<img id="img5" border="rounded" src="/img/bot5.jpg" /><br>Vinculación del token<img id="img6" border="rounded" src="/img/bot6.jpg" />
</div>
</center>

<style>
#img5{
  width:510px;
  height:240px;
}
#img6{
  width:330px;
  height:160px;
}
</style>

---

# Resultados

Las pruebas se realizaron por medio de **Telegram** desde un dispositivo móvil, aplicación web y desde su aplicación de escritorio.
<center>
<tr>
<td>
<img id="web" src="/img/escritorio.png"/>
</td>
<td>
<img id="movil" src="/img/movil.jpeg"/>
</td>
</tr>
</center>

<style>
#web{
  width:500px;
  height:300px;
}
#movil{
  width:200px;
  height:330px;
}
</style>

---

# Conclusiones

<p>
Al termino del proyecto se han obtenido conocimientos acerca de la inteligencia artificial así como el procesamiento del lenguaje natural y el aprendizaje autónomo. 
Con estos conocimientos se llevo con exito el <strong>Chatbot</strong> el cual ayudará a los usuarios del ITGAM a poder informarce de las distintas dudas que ellos tengan acerca de las dudas que ellos tengan. 
</p>

<center>
<img id="qr" border="rounded" src="/img/qr.png"/>
</center>

<style>
p{
  text-align:justify;
}
#qr{
  width:250px;
  height:330px;
}
</style>

<style>
.footnotes-sep {
  @apply mt-20 opacity-10;
}
.footnotes {
  @apply text-sm opacity-75;
}
.footnote-backref {
  display: none;
}

.card_information {
  box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
  transition: 0.3s;
  margin: 8px;
}

.card {
  box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
  width: 300px;
  height: 150px;
  transition: 0.3s;
  margin: 8px;
}

/* On mouse-over, add a deeper shadow */
.card:hover {
  box-shadow: 0 8px 16px 0 rgba(0,0,0,0.2);
}

/* Add some padding inside the card container */
.container {
  padding: 2px 16px;
}

.img_size {
width: 10px;
  height: 10px;
}

.container-cards {
  max-width: 100%;
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  flex-wrap: no-wrap;
  align-items: center;
  align-content: space-between;
}

.container-column {
  max-width: 100%;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  flex-wrap: no-wrap;
  align-items: center;
  align-content: space-between;
}
</style>

