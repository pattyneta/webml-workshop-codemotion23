# ¡Bienvenid@ al taller de reconocimiento de emociones!

## Actualiza el código importado de Teachable Machine

1. Sigue estos pasos:

- Clona este repositorio
- Ve al directorio raiz
- Ejecuta ```npm install```
- Ejecuta ```npm test```
- Siga las instrucciones en la presentación

2. Abre index.html y ubica el comentario donde debes pegar el código de Teachable Machine, ahora editaras ese mismo código que acabas de pegar.

3. Elimina las siguientes líneas:
  ```
  <div>Teachable Machine Image Model</div>
  <button type="button" onclick="init()">Start</button>
  <div id="webcam-container"></div>
  <div id="label-container"></div>/div>
  ```
4. Bajo la línea que contiene la URL importada, copie el siguiente código:

    ```
    let robotContainter = document.getElementById("robot-container");
    let robotFace = document.createElement("img");
    let robotTalk = document.createElement("p");
    robotTalk.innerText = "No entiendo a los humanos... *suspiro*"
    robotFace.src = "/images/waiting.png";
    robotContainter.appendChild(robotFace);
    robotContainter.appendChild(robotTalk);
    ```
5. Luego, en el mismo archivo, reemplaza el contenido de la función predict() con el siguiente código::

      
        // predict puede tomar una imagen, video o elemento canvas html
        const prediction = await model.predict(webcam.canvas);
        for (let i = 0; i < maxPredictions; i++) {
            const classPrediction =
                prediction[i].className + ": " + prediction[i].probability.toFixed(2);
            labelContainer.childNodes[i].innerHTML = classPrediction;
            if ((prediction[i].className === 'happy') && (prediction[i].probability.toFixed(2) >= 0.90)) {
                robotFace.src = "/images/happy.png";
                robotTalk.innerText = "¡Me encanta verte tan feliz!"
            } else if ((prediction[i].className === 'angry') && (prediction[i].probability.toFixed(2) >= 0.90)) {
                robotFace.src = "/images/angry.png";
                robotTalk.innerText = "¡Destruir! ¡Destruir! ¡Destruir!"
            }
            robotContainter.appendChild(robotFace);
            robotContainter.appendChild(robotTalk);
        }
      
