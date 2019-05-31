---
title: "Coding a simple poker game on python"
date: 2019-05-29T06:42:00-04:00
---

In this game of poker, the rules are simple: the user will input the number of players into the code as an argument. The script will as the names of every player, then deal 5 cards each. In this version of the game, we just compare the hands, and the hand with the highest card wins. In the case of a tie where multiple players have the same highest card, it script will revert to each player's second highest card to compare. For example, if player 1 has the hand 2, 3, K, Q, 7, and player 2 has the hand J, J, K, 7, 3, then player 1 would win because K, Q beats K, J.

So, to start, we will be using the random module, so import random is required. In this game, the function would accept one argument -- the number_of_players. Then, the first line of the program would ask for each players' name. Since this has to be asked the same number of times as how many players there are, a for loop is involved. I made these names form a list so later it would be easier to access each name by indexing the list. The first line would be: names = [ input( "Please enter your name: " for i in range( number_of_players ) ) ].

Next, we would have to set up the game. This involves giving the options for cards to be dealt to each player. I made a list of each available card: cards = [ "A", "K", "Q", "J", "10", "9", "8", "7", "6", "5", "4", "3", "2" ] * 4. The list was multiplied by 4 because there are four different suits, so each number could be drawn out 4 times. To be able to compare these values later to determine the winner, a dictionary of values would also have to be made so the cards drawn out would be able to be compared against one another to see which one is higher: values = {"2": 2, "3": 3, "4": 4, "5": 5, "6": 6, "7": 7, "8": 8, "9": 9, "10": 10, "J": 11,"Q": 12,"K": 13,"A": 14}. The final steps of setting up would be to make empty dictionaries of the hand and ordered hand: hand = {}; ordered_hand = {}. The hand represents the cards dealt to each player, and the ordered_hand represents the cards dealt to each player converted to their values and in a descending order.

Now that the game is set, we can start dealing the cards. Each player will receive 5 cards. Since the game can be used with any number of players, a for loop is required and it will have to use what the user inputted: for name in names:. The aim is to have the keys in the hand and ordered_hand dictionary be the players' names, and the values to be a list of their cards. So, the list for the cards for each player will have to be initialized: hand[ name ] = []; ordered_hand = []. Now for dealing cards. Since each player is dealt 5 cards, a for loop can be created under the previous for loop: for i in range( 0, 5 ):. The cards dealt should be random from the list of cards: choice = random.choice( cards ). This value will then need to be appended to the list of cards chosen for that particular player: hand[ name ] += [ choice ]. If we print( hand ) at this point, it should output a dictionary of the players and cards, eg. { 'a': [ '4', '6', '2', 'J', 'A' ], 'b': [ '9', 'Q', '6', '2', 'K' ] }. To make this easy to compare, we should convert these strings into numerical values using the values dictionary. So, under the same for loop because we want to convert each one of the cards: value = values.get( choice ). We then append this value to the ordered_hand dictionary, similar to how the original card choice was appended to the hand dictionary: ordered_hand += [ value ]. We then want to remove this card from the list of cards available to choose from so the script does not dealt more than four of each card number. We now have a dictionary of the cards for each player converted into their values, eg. { 'a': [ 4, 6, 2, 11, 14 ], 'b': [ 9, 12, 6, 2, 13 ] }. We can now get out of this for loop, but make sure to still stay in the first one. We want to print out each players' hand, so we can format a code within the for loop of the players: print( "{}'s hand is {}, {}, {}, {}, {}.".format( name, hand[ name ][ 0 ], hand[ name ][ 1 ], hand[ name ][ 2 ], hand[ name ][ 3 ], hand[ name ][ 4 ])).

To compare each player's hand to determine the winner, we need to sort the cards of each player. Since it has to be done for each player, we should stay within the same for loop and reference each list in the dictionary separately: ordered_hand[ name ].sort( reverse = True ). We need to initialize another dictionary which the key with the maximum value will have: compare = {}. The next step would be to code a mapping into the dictionary, then compare other values to it. If the value is bigger than what compare has, it will replace it.

for name, value in ordered_hand.items():
    if not compare:
        compare[ name ] = values
        continue
    for i in range( 5 ):
        if value[ i ] == list( compare.values() )[ 0 ][ i ]:
            continue
        elif value[ i ] > list( compare.values() )[ 0 ][ i ]:
          compare = { name: value }
          break
    break

The final step would be to print out the winner which would be the only key in the dictionary. result = "The winner is {}.".format( list( compare.keys() )[ 0 ] ). Then return result. The game is finished.
