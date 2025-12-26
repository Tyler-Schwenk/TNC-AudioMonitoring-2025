# Alternative Methodologies Explored

I initiated preliminary explorations into other training techniques to identify potential future areas for development

* [Focus on specific call type](separate-call-types.md)
  * In this experimental stage, I briefly explored the idea of training the model to identify specific types of the California red-legged frog's call, rather than both as the same label.
* [Reduced Frequency Models](reduced-max-frequency-models.md)
  * This showed promise in its ability to work with data at a reduced file size while retaining comparable metrics.
* [Appended labels](appended-labels.md)
  * This explores the idea of appending our classifier head on top of the standard BirdNET classifier - retaining the ability to identify the 6,000+ standard species on top of our custom class.&#x20;
* [Human In the Loop (HITL)](human-in-the-loop.md)
  * Standard HITL training was not applicable to our strongly labelled data, but promised to help provide improvements to future models with minimal effort.

