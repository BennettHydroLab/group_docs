# Tutorials and how-tos

## Useful snippets

- Testing if your PyTorch installation has CUDA correctly installed: `python -c "import torch; print(torch.cuda.is_available())"`
- Showing the size of all files/folders in your current directory `for d in $(ls); do du -sh $d; done`

## Made by the group
This section is for resources which have been created by members or close collaborators.

- [High resolution predictions of global snow using recurrent neural networks](https://github.com/geo-smart/global_lstm_swe_modeling#high-resolution-predictions-of-global-snow-using-recurrent-neural-networks): This is a machine learning tutorial that highlights using large-scale climate projections and recurrent neural networks to model snow.
- [AI for physics-inspired hydrology modeling](https://www.sciencedirect.com/science/article/abs/pii/B9780323917377000062?via%3Dihub): An end to end implementation of hybrid modeling techniques that blend machine learning with differential equations for hydrologic modeling. Open source implementation [here](https://github.com/earth-artificial-intelligence/earth_ai_book_materials/tree/main/chapter_07).

## From around the web
### Visualization

- [20 simple, distinct colors](https://sashamaps.net/docs/resources/20-colors/): A simple, interactive tool to picking basic colors for data visualization.
- [Color Brewer](https://colorbrewer2.org/#type=sequential&scheme=BuGn&n=3): Color advice for cartography

### Machine Learning

- [A Recipe for Training Neural Networks](http://karpathy.github.io/2019/04/25/recipe/): Practical (and often unspoken) advice for how to train deep learning models in the wild.
- [Understanding LSTM Networks](https://colah.github.io/posts/2015-08-Understanding-LSTMs/): An illustrated guide to understanding Long-Short Term Memory Networks, a popular variant of recurrent neural networks for environmental timeseries modeling.
