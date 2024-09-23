#  cs61b_proj0完成后思考——通过旋转棋盘来实现向四个方向移动的逻辑

昨天写完了cs61b的proj0：2048，项目很简单，总体上就是写好两部分的逻辑，一是游戏面板（Board）（或者说棋盘更好理解一点），二是数字块（Tile）的移动逻辑。

游戏面板方面，只有两个逻辑要写，一是判断面板上是否还有空位（Empty Space Exists），二是判断游戏是否结束（Max Tile Exists/At Least One Move Exists）,没什么好说的。

数字块移动逻辑的实现方面很有意思，共有四个移动方向（上下左右），每次移动时，每一行/列的所有可移动数字块都会向选定方向移动，这是2048游戏的数字块移动逻辑。在具体实现过程中，分三步完成了向某一方向（这里默认为向上）移动逻辑的实现：Step1：Move Tile Up（移动一个数字块）；Step2：Tilt Column（移动一列数字块）；Step3：Tilt Up（移动所有数字块）。这是编程过程中的经典操作，即将大问题分解为小问题，在逻辑上逐层递进，逐个击破。这是编程经典思路，在这里不多赘述。

最让我感到惊喜的是向四个方向移动过程的实现代码。由于数字块向四个方向移动的逻辑都是一样的，而我们在上一段通过三个方法（method）已经完成了向上移动逻辑的编写，那么我们其实可以通过旋转游戏面板来完成向其它三个方向移动逻辑的编写。这是通过引入属性“视角”（viewPerspective）来实现的（所以其实是以玩家视角的转变完成游戏面板的旋转），这样使得代码更简洁且更易维护。

## 在CS61b项目文档中相关表述如下：

### Task 9: Tilt in Four Directions

Now that we've gotten tilt working for the up direction, we have to do the same thing for the other three directions.

One possible approach is to copy-paste our code four times, and slightly change a few lines to handle the other three directions. This leads to messy, hard-to-read code, with ample opportunity to introduce obscure bugs. What if you fix something in one copy, but not the other three copies?

For this problem, we've given away a clean solution. This will allow you to handle the other three directions with only two additional lines of code!

#### Starter code: Side

The Side class is a special type of class called an Enum. Enums may take on only one of a finite set of values. In this case, we have a value for each of the 4 sides: NORTH, SOUTH, EAST, and WEST. You will not need to use any of the methods of this class nor manipulate the instance variables.

Enums can be assigned with syntax like Side s = Side.NORTH. Note that rather than using the new keyword, we simply set the Side value equal to one of the four values. Similarly if we have a function like public static void printSide(Side s), we can call this function as follows: printSide(Side.NORTH), which will pass the value NORTH to the function.

If you're curious to learn more about Java enums, see https://docs.oracle.com/javase/tutorial/java/javaOO/enum.html .

Starter code: setViewingPerspective method in Board
Specifically, the Board class has a setViewingPerspective(Side s) function that will change the behavior of the tile and move classes so that they behave as if the given side was NORTH.

For example, consider the board below:

|    |    |    |    |
|  16|    |  16|    |
|    |    |    |    |
|    |    |    |   2|

If we call board.tile(0, 2), we'll get 16, since 16 is in column 0, row 2. If we call board.setViewingPerspective(s) where s is WEST, then the board will behave as if WEST was NORTH, i.e. you had your head turned 90 degrees to the left, as shown below:

|    |    |  16|    |
|    |    |    |    |
|    |    |  16|    |
|   2|    |    |    |

In other words, the 16 we had before would be at board.tile(2, 3). If we were to call board.tilt(Side.NORTH) with a properly implemented tilt, the board would become:

|   2|    |  32|    |
|    |    |    |    |
|    |    |    |    |
|    |    |    |    |

To get the board to go back to the original viewing perspective, we simply call board.setViewingPerspective(Side.NORTH), which will make the board behave as if NORTH was NORTH. If we do this, the board will now behave as if it were:

|    |    |    |    |
|  32|    |    |    |
|    |    |    |    |
|   2|    |    |    |

Observe that this is the same thing as if you'd slid the tiles of the original board to the WEST.

Important: Make sure to use board.setViewingPerspective to set the perspective back to Side.NORTH before you finish your call to tilt, otherwise weird stuff will happen.




     










