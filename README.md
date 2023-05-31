# toptrumps
# import all libraries that I need for this project

import random
import requests

# import sleep from time in order to give the game a better flow by delaying print statements

from time import sleep


# def game will allow me to manipulate the whole code later on

def game():

    # API get request used to retrieve data from the pokemon API
    # using .randint I am able to call a random number
    # adding .format to the api url, I can obtain a random pokemon

    def random_pokemon():
        pokemon_number = random.randint(1, 151)
        url = 'https://pokeapi.co/api/v2/pokemon/{}/'.format(pokemon_number)
        response = requests.get(url)
        pokemon = response.json()

        # return all values that will be used for comparison in the top trumps game
        # some values are nested in the API so use [], [] to grab values
        # use .title() to capitalise the pokemons name

        return {
            'name': pokemon['name'].title(),
            'id': pokemon['id'],
            'height': pokemon['height'],
            'weight': pokemon['weight'],
            'hp': pokemon['stats'][0]['base_stat'],
            'attack': pokemon['stats'][1]['base_stat'],
            'defense': pokemon['stats'][2]['base_stat']
        }

    def run():
        my_pokemon = random_pokemon()
        print('Welcome to the world of Pokemon! \n')

        # example of sleep usage to delay printing
        sleep(2)

        player = input('What is your name? \n')

        sleep(1)

        print('Hello {}!'.format(player.title()))

        sleep(1)

        print('You were given', my_pokemon['name'])

        sleep(1)

        # use '\n' to put attributes in the print statement on separate lines
        # use '.format{my_pokemon['ATTRIBUTE']} to populate the top trumps 'card' so the player is able to make a
        # clearer decision on which attribute to select

        print(
            "Your Pokemon's stats are: \n ID: {} \n Height: {} \n Weight: {} \n HP: {} \n Attack: {} \n Defense: {}".format(
                my_pokemon['id'], my_pokemon['height'], my_pokemon['weight'], my_pokemon['hp'], my_pokemon['attack'],
                my_pokemon['defense']))

        sleep(2)

        stat_choice = input('Which stat do you want to use? (id, height, weight, hp, attack, defense) \n')

        opponent_pokemon = random_pokemon()

        print('The opponent chose {}'.format(opponent_pokemon['name']))

        my_stat = my_pokemon[stat_choice.lower()]
        opponent_stat = opponent_pokemon[stat_choice.lower()]

        sleep(0.5)

        print('Calculating result...')

        sleep(2.5)

        # logic to determine who wins

        if my_stat > opponent_stat:
            print('{} Wins!'.format(player.title()))
        elif my_stat < opponent_stat:
            print('You Lose!')
        else:
            print('Draw!')

    run()


game()

# using a while loop to allow player to restart the game

play_again = input('Would you like to play again? Please enter Yes or No \n').lower()
while play_again == 'Yes':
    game()
if play_again != 'Yes':
    sleep(0.5)
    print('See you next time!')
