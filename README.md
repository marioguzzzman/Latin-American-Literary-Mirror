# Learning to Write / Espejo Literario Latinoamericano (2019)

A textual artificial organism that performs a reading and writing exercise: a neural network watches video from around the globe, and a language model trained on 19th-century travel literature narrates what it thinks is happening.

**▶ [Watch the piece (Vimeo)](https://player.vimeo.com/video/390603479)** · [Project page](https://www.mario-guzman.com/project/learningtowrite.html)

<!-- PUNCH LIST: add a still from the Vimeo video as docs/hero.jpg -->

Shown at **Game on! El arte en juego** (Centro Cultural San Martín, Buenos Aires, 2019) and **Mixed Feelings, School of Machines, Making & Make-Believe** (Berlin, 2019).

## About the piece

**EN:**
The work arises from a need to organize a series of chaotic experiences while traveling to more than 39 countries and 1,532 flight hours with a social robot. To make sense of the speed and heterogeneity of these episodes, it articulates two structures into a writing system: a convolutional neural network using mobile vision interprets audiovisual micro-narratives — personal waiting times, moments of presence — and the objects and situations it recognizes are sent to an LSTM recurrent network trained on 19th-century travel literature, which narrates what is happening, or what it thinks is happening, in the image. The work is an experiment around an endless writing action that tries to understand a world constituted by limited objects and perceptions — perhaps a reflection of our own cognitive operations. In its Spanish configuration, *Espejo Literario Latinoamericano*, the system writes through a model trained on Latin American literature instead.

**ES:**
La obra surge de la necesidad de organizar una serie de experiencias caóticas tras viajar por más de 39 países y 1,532 horas de vuelo con un robot social. Para dar sentido a la velocidad y heterogeneidad de esos episodios, articula dos estructuras en un sistema de escritura: una red neuronal convolucional de visión móvil interpreta micro-narrativas audiovisuales —tiempos de espera personales, momentos de presencia— y los objetos y situaciones que reconoce se envían a una red recurrente LSTM entrenada con literatura de viajes del siglo XIX, que narra lo que sucede —o lo que cree que sucede— en la imagen. La obra es un experimento en torno a una acción de escritura interminable que intenta comprender un mundo constituido por objetos y percepciones limitados; quizá un reflejo de nuestras propias operaciones cognitivas. En su configuración en español, *Espejo Literario Latinoamericano*, el sistema escribe a través de un modelo entrenado con literatura latinoamericana.

## How it works

Browser piece built on p5.js + ml5.js (runs locally, no build step):

1. **See** — webcam or video feeds ml5's MobileNet image classifier (`Scripts/mobileNetScript.js`); the top label is extracted.
2. **Write** — the label seeds an ml5 charRNN (LSTM) with random output length and temperature 0.9. Trained models live in `test-lstm/`: `data-travel-long` (19th-century travel chronicles — Darwin, Humboldt, Twain, Marco Polo; corpus list in `Notes/list_of_texts_lstm.txt`) and `model_8_latin` (Latin American literature), alongside ml5's stock author models used during testing.
3. **Mirror (ES mode)** — with `translate = true`, the label is translated EN→ES (`Scripts/translatorScript.js`) and the Latin American model writes in Spanish; with `translate = false` the travel-literature model writes in English.
4. **Show & speak** — generated text renders as a fake terminal and as subtitles over found travel video with pixel/glitch effects (`videosOrginalFuncional.js`, the main sketch); p5.speech reads it aloud (Spanish voice at lowered rate and pitch). The page auto-refreshes every 500 s to keep long installations responsive.
5. **Train** — `training-lstm/` holds the TensorFlow char-RNN training code used to produce the models (run on cloud GPUs; see `register_photos/` for process documentation).

`arduino_tests/` holds joystick-interaction experiments that didn't make it into the final piece.

## Running it

Requires a webcam and Chrome (the piece does not work in Firefox):

1. Serve the folder: `python3 -m http.server` and open `http://localhost:8000/`.
2. The Spanish mirror mode requires a Google Translate API key — create your own and load it from an untracked `config.js`, or set `translate = false` in `videosOrginalFuncional.js` for the English travel-literature mode.
3. Behavior toggles (one video vs. random videos, camera modes, effects) are the flag block at the top of `videosOrginalFuncional.js`; some combinations are marked non-working in the comments and are kept as-is.

