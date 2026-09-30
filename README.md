# Regional Pokémon Team Builder

A Streamlit web application for building and managing a Pokémon team based on regional Pokédex data. The application uses the [PokéAPI](https://pokeapi.co/) to retrieve Pokémon information, forms, abilities, moves, and base stats.

## Features

* **Regional Pokémon selection**

  * Choose from Kanto, Johto, Hoenn, Sinnoh, Unova, Kalos, Alola, Galar, or Paldea.
  * View Pokémon native to the selected region.
  * Optionally show only Pokémon newly introduced in that region.

* **Pokémon information**

  * View Pokémon sprites, types, abilities, and hidden abilities.
  * Select from available Pokémon forms.
  * View level-up learnable moves.
  * View base-stat distributions using a radar chart and table.

* **Team building**

  * Add Pokémon to a personal team.
  * Teams are limited to six Pokémon.
  * Remove individual Pokémon from the team.
  * Clear the entire team.

* **Team persistence**

  * The current team is saved to `data/team.csv`.
  * Regional Pokémon lists are cached in JSON files under `data/` to reduce repeated API requests.

* **Team visualization**

  * View the type distribution of the current team with a Plotly bar chart.

* **Additional interface features**

  * Pokémon can be sorted numerically or alphabetically.
  * A map can be displayed in the Introduction page using Streamlit's map component.
  * Pokémon type badges use type-specific colors.

## Technologies Used

* **Python**
* **Streamlit** — web application interface
* **PokéAPI** — Pokémon data source
* **Pandas** — tabular data and CSV handling
* **Plotly** — charts and Pokémon stat visualization
* **Requests** — API requests
* **JSON** — cached Pokémon data
* **Concurrent futures** — parallel API requests
* **functools** — caching Pokémon IDs

## Project Structure

```text
project/
├── app.py
├── data/
│   ├── team.csv
│   ├── native_<region>.json
│   └── new_<region>.json
└── README.md
```

> The `data/` directory is created automatically by the application if it does not already exist.

## Requirements

Python 3.9+ is recommended.

Install the required Python packages with:

```bash
pip install streamlit requests pandas plotly
```

## Running the Application

1. Clone or download the project.

2. Open a terminal in the project directory.

3. Install the dependencies:

```bash
pip install streamlit requests pandas plotly
```

4. Start the Streamlit application:

```bash
streamlit run app.py
```

5. Open the local URL provided by Streamlit in your browser.

## How to Use

### 1. Introduction

The **Introduction** page provides a short overview of the application.

There is also an optional map feature. Check the map consent box, choose a color, and press **Confirm** to display the map.

### 2. Create a Team

Select **Create a Team** from the sidebar.

1. Choose a Pokémon region.
2. Choose whether to display only newly introduced Pokémon.
3. Choose a sorting method:

   * Numerical
   * Alphabetical
4. Select a Pokémon.
5. Review its information.
6. If multiple forms are available, select the desired form.
7. Press **Add to My Team**.

A team can contain a maximum of **six Pokémon**.

### 3. View Pokémon Information

For a selected Pokémon, the application can display:

* Sprite
* Pokémon name
* Types
* Abilities
* Hidden abilities
* Learnable level-up moves
* Base-stat radar chart
* Base-stat table and total

### 4. View Teams

The **View Teams** page displays the current team and allows individual Pokémon to be removed.

You can also select **Clear Entire Team** to remove the saved team.

When Pokémon are present, a **Team Type Distribution** chart shows how many Pokémon on the team have each type.

## Data and API

The application retrieves Pokémon information from PokéAPI:

```text
https://pokeapi.co/api/v2/
```

The application uses several PokéAPI endpoints, including:

```text
/pokemon/{pokemon}
/pokemon-species/{species}
/region/{region}
/generation/{generation}
```

API results are cached with Streamlit's `@st.cache_data` where appropriate. Regional Pokémon lists are also stored locally as JSON files after they are generated.

## Caching

The first time a regional Pokémon list is generated, the application may take longer because it makes multiple API requests.

Generated lists are saved in the `data/` directory:

```text
data/native_kanto.json
data/native_johto.json
...
data/new_kanto.json
data/new_johto.json
...
```

On later runs, the application can load these cached files instead of generating the lists again.

## Team Storage

The current team is stored in:

```text
data/team.csv
```

Each team entry stores information such as:

* Pokémon display name
* API name
* Pokémon types

The application loads the saved team when the **Create a Team** page is opened and updates the CSV when Pokémon are removed or the team is cleared.

## Pokémon Forms

The application handles several types of Pokémon forms, including regional forms such as:

* Alolan
* Galarian
* Hisuian
* Paldean

It also contains special handling for forms such as Mega Evolutions, Gigantamax forms, Pikachu forms, and Eevee forms.

Pokémon names are formatted for display so API names such as:

```text
mr-mime
```

can be displayed
