# Can Convolutional Neural Networks Crack Sudoku Puzzles?

This project is motivated simply by my personal curiosity--can CNNs crack learn how to solve Sudoku? There are many computational approaches to do that. Why not neural networks?

## Requirements
  * numpy >= 1.11.1
  * sugartensor >= 0.0.1.8 (pip install sugartensor)
	
## Research Question
Can Convolutional Neural Networks Crack Sudoku Puzzles?

## Background
* To see what Sudoku is, check the wikipedia [here](https://en.wikipedia.org/wiki/Sudoku)
* To investigate this task comprehensively, read through [McGuire et al. 2013](https://arxiv.org/pdf/1201.0749.pdf)

## Workflow
* STEP 1. Generate [1M games of Sudoku](https://drive.google.com/open?id=0B0ZXk88koS2Ka0lVQWtBTUhWbUU). (=Y) (See `generate_sudoku.py`)<br/>
* STEP 2. Make [1, 65] blanks randomly with uniform probabilities for every cell. (=X) (See `load_data` in `train.py`)<br/>
* STEP 3. Build convolutional networks as follows. (See `Graph` in `train.py`)<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;5 convolutional layers of 512 dimensions<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;1 final convolutional layer with a 1 by 1 filter.<br/>
STEP 4. Train the model, feeding X and Y. Loss is calucated from the predictions for the blanks. (See `train.py`)<br/>
STEP 5. Evaluate (See `test.py`).

## Results
After 10 epochs, we got [this model file](https://drive.google.com/open?id=0B0ZXk88koS2KR0hETzI4dVdZV0k). Subsequently, we evaluated according to the following two methods.

* Test method 1: Predict the numbers in blanks all at once.
* Test method 2: Predict the numbers sequentially from the most confident one at each step.

 
| Level  |  Test1 <br/>(#correct/#blanks=acc.)| Test2 <br/>(#correct/#blanks=acc.) |
| ---    |---     |---     |
|Easy|25/47=0.53|27/47=0.57|
|Easy|26/45=0.58|29/45=0.64|
|Easy|29/47=0.62|37/47=0.79|
|Easy|24/45=0.53|24/45=0.53|
|Easy|25/47=0.53|35/47=0.74|
|Easy|23/46=0.50|30/46=0.65|
|Medium|17/53=0.32|9/53=0.17|
|Medium|20/55=0.36|13/55=0.24|
|Medium|17/55=0.31|16/55=0.29|
|Medium|25/53=0.47|39/53=0.74|
|Medium|25/52=0.48|32/52=0.62|
|Medium|28/56=0.50|12/56=0.21|
|Hard|18/56=0.32|12/56=0.21|
|Hard|19/55=0.35|14/55=0.25|
|Hard|19/55=0.35|21/55=0.38|
|Hard|22/57=0.39|16/57=0.28|
|Hard|26/55=0.47|9/55=0.16|
|Hard|25/56=0.45|36/56=0.64|
|Expert|21/56=0.38|19/56=0.34|
|Expert|22/55=0.40|25/55=0.45|
|Expert|20/54=0.37|12/54=0.22|
|Expert|25/55=0.45|25/55=0.45|
|Expert|23/55=0.42|20/55=0.36|
|Expert|24/54=0.44|19/54=0.35|
|Evil|28/50=0.56|38/50=0.76|
|Evil|20/50=0.40|26/50=0.52|
|Evil|26/49=0.53|29/49=0.59|
|Evil|21/53=0.40|17/53=0.32|
|Evil|23/51=0.45|15/51=0.29|
|Evil|26/51=0.51|16/51=0.31|
Total Accuracy| 692/1568=0.44|672/1568=0.43|

## Conclusions
* I also tested fully connected layers, to no avail.
* Up to some point, it seems that CNNs can learn to solve Sudoku.
* For some problems, the second method was more effective than the first method. But I can't figure out more about that.
* Probably reinforcement learning would be more appropriate for Sudoku solving.

## Notes for reproducibility
* Download pre-generated Sudoku games [here](https://drive.google.com/open?id=0B0ZXk88koS2Ka0lVQWtBTUhWbUU) and extract it to `data/` folder.
* Download pre-trained model file [here](https://drive.google.com/open?id=0B0ZXk88koS2KR0hETzI4dVdZV0k) and extract it to `asset/train/ckpt` folder.
	






