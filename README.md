# Project-1
outline of my final project 

import ipywidgets as widgets
from IPython.display import display
import random

# Created dataset of 25 players with stats
player_names = [
    "Antoine Dupont", "Ardie Savea", "Cheslin Kolbe", "Eben Etzebeth", "Marcus Smith",
    "Beauden Barrett", "Romain Ntamack", "Maro Itoje", "Siya Kolisi", "Finn Russell",
    "Aaron Smith", "Richie Mo'unga", "James Ryan", "Caelan Doris", "Damian Penaud",
    "Freddie Steward", "Ellis Genge", "Tadhg Furlong", "Tom Curry", "Sam Cane",
    "Pieter-Steph Du Toit", "Will Jordan", "Josh van der Flier", "Courtney Lawes", "Duhan van der Merwe"
]

# Generate stats for each player
top_25_rugby_players = {
    name: {
        "tries": random.randint(3, 15),
        "tackles": random.randint(50, 150),
        "meters_gained": random.randint(200, 600),
        "kicking_accuracy": random.randint(60, 100)
    } for name in player_names
}

# List of available stats
available_stats = list(next(iter(top_25_rugby_players.values())).keys())

# Widgets
player_selector = widgets.SelectMultiple(
    options=player_names,
    description='Players',
    rows=10,
    disabled=False
)

stat_selector = widgets.Dropdown(
    options=available_stats,
    description='Stat',
    disabled=False
)

button = widgets.Button(description="Show Stat")

# Button click logic
def on_button_click(b):
    selected_stat = stat_selector.value
    selected_players = player_selector.value

    print(f" Showing '{selected_stat}' for selected players:\n")
    for player in selected_players:
        stat_value = top_25_rugby_players[player].get(selected_stat, "N/A")
        print(f"{player}: {stat_value}")
    print("-" * 40)

button.on_click(on_button_click)

# Display widgets
display(player_selector, stat_selector, button)
