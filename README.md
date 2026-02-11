# My Teachable Machine Model

![Teachable Machine](https://img.shields.io/badge/Teachable%20Machine-Image%20Model-blue)

This repository contains a machine learning model created using [Google's Teachable Machine](https://teachablemachine.withgoogle.com/).

## 🔗 Model Link
The model is hosted online and can be accessed here:  
**[https://teachablemachine.withgoogle.com/models/KWtcPPLV0/](https://teachablemachine.withgoogle.com/models/KWtcPPLV0/)**

## 🤖 Description
This model was trained to detect and classify specific objects or scenarios. It runs entirely in the browser using TensorFlow.js.

### Classes
The model has been trained to recognize the following classes:
1. **[Class Name 1]** - (e.g., "Glove")
2. **[Class Name 2]** - (e.g., "Cell phone")
3. **[Class Name 3]** - (e.g., "Blank (any color)")
*(Edit this list to match your specific model labels)*

## 🛠️ How to Use

You can use this model in your own web application using JavaScript.

### 1. HTML Setup
Add the TensorFlow.js library and the Teachable Machine library to your `index.html` file:

```html
<div>Teachable Machine Image Model</div>
<button type="button" onclick="init()">Start</button>
<div id="webcam-container"></div>
<div id="label-container"></div>

<script src="[https://cdn.jsdelivr.net/npm/@tensorflow/tfjs@latest/dist/tf.min.js](https://cdn.jsdelivr.net/npm/@tensorflow/tfjs@latest/dist/tf.min.js)"></script>
<script src="[https://cdn.jsdelivr.net/npm/@teachablemachine/image@latest/dist/teachablemachine-image.min.js](https://cdn.jsdelivr.net/npm/@teachablemachine/image@latest/dist/teachablemachine-image.min.js)"></script>
<script type="text/javascript">
    // More API functions here:
    // [https://github.com/googlecreativelab/teachablemachine-community/tree/master/libraries/image](https://github.com/googlecreativelab/teachablemachine-community/tree/master/libraries/image)

    // the link to your model provided by Teachable Machine export panel
    const URL = "[https://teachablemachine.withgoogle.com/models/KWtcPPLV0/](https://teachablemachine.withgoogle.com/models/KWtcPPLV0/)";

    let model, webcam, labelContainer, maxPredictions;

    // Load the image model and setup the webcam
    async function init() {
        const modelURL = URL + "model.json";
        const metadataURL = URL + "metadata.json";

        // load the model and metadata
        model = await tmImage.load(modelURL, metadataURL);
        maxPredictions = model.getTotalClasses();

        // Convenience function to setup a webcam
        const flip = true; // whether to flip the webcam
        webcam = new tmImage.Webcam(200, 200, flip); // width, height, flip
        await webcam.setup(); // request access to the webcam
        await webcam.play();
        window.requestAnimationFrame(loop);

        // append elements to the DOM
        document.getElementById("webcam-container").appendChild(webcam.canvas);
        labelContainer = document.getElementById("label-container");
        for (let i = 0; i < maxPredictions; i++) { // and class labels
            labelContainer.appendChild(document.createElement("div"));
        }
    }

### Proof of My trained Model

<img width="196" height="332" alt="image" src="https://github.com/user-attachments/assets/6a981f35-d118-4ed4-89c0-e6aeb129d88f" />



<img width="182" height="328" alt="image" src="https://github.com/user-attachments/assets/21d0ed75-7bbf-4002-8a3a-1f82f1c98fd7" />



<img width="180" height="329" alt="image" src="https://github.com/user-attachments/assets/429137f9-3246-42e3-8025-11955a9d935f" />






    async function loop() {
        webcam.update(); // update the webcam frame
        await predict();
        window.requestAnimationFrame(loop);
    }

    // run the webcam image through the image model
    async function predict() {
        // predict can take in an image, video or canvas html element
        const prediction = await model.predict(webcam.canvas);
        for (let i = 0; i < maxPredictions; i++) {
            const classPrediction =
                prediction[i].className + ": " + prediction[i].probability.toFixed(2);
            labelContainer.childNodes[i].innerHTML = classPrediction;
        }
    }
</script># Teachable-Machine
Machine Learning
