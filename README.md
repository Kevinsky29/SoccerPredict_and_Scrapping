# SoccerPredict and Scrapping

## Tabla de Contenidos
- [Descripción](#descripción)
- [Funciones para recopilar datos de equipos](#funciones-para-recopilar-datos-de-equipos)
- [Uso](#uso)
- [Resultados](#resultados)
- [Archivos generados](#archivos-generados)
- [Contribución](#contribución)
- [Licencia](#licencia)

## Descripción
Este proyecto contiene scripts robustos de Python que utilizan técnicas de web scraping para recopilar datos detallados de partidos de fútbol de diversas fuentes en la web. Con un enfoque en ligas y torneos internacionales importantes, los datos recopilados abarcan varias categorías, incluyendo estadísticas de jugadores, rendimiento de equipos, resultados históricos y mucho más.

## Funciones para recopilar datos de equipos

El archivo `TeamScraper.py` contiene una clase `TeamScraper` que proporciona funciones para realizar web scraping y obtener datos de equipos. A continuación se muestra un ejemplo de cómo utilizar estas funciones:

```python
year_seasons = [2014, 2015, 2016, 2017, 2018, 2019, 2020, 2021, 2022]
team = input('Enter the team name:')

season_dfs = []
player_dfs = []
matches_dfs = []

for year_season in year_seasons:
    team_scraper = TeamScraper(team, year_season)

    team_data = team_scraper.scrape_team_data()
    season_dfs.append(team_data)

    team_players, team_name = team_scraper.scrape_team_players()
    player_dfs.append(team_players)

    filename = f"{team}_{year_season}.csv"
    match_data, data_names = team_scraper.read_match_data(filename)

    df_matches = team_scraper.convert_to_dataframe(data_names)
    df_matches['season'] = f"{str(year_season)}/{str(year_season + 1)}"

    matches_dfs.append(df_matches)

all_matches_df = pd.concat(matches_dfs)
all_matches_df.to_csv('MC_matches.csv', index=False)
df_compiled = pd.concat(season_dfs)
df_compiled.to_csv('MC_seasons.csv', index=False)
df_compiled_players = pd.concat(player_dfs)
df_compiled_players.to_csv('MC_players.csv', index=False)
```
## Ligas Disponibles

A continuación se muestra una lista de las ligas disponibles actualmente en el proyecto:

### Premier League
![Premier League](/images_ligues/premier_league.png)

### La Liga
![La Liga](/images_ligues/LaLiga.png)

### Serie A
![Serie A](/images_ligues/Seria_A.png)

### Bundesliga
![Bundesliga](/images_ligues/Bundesliga.png)

### Ligue 1
![Ligue 1](/images_ligues/Ligue1.png)

Puedes seleccionar una liga específica para recopilar datos utilizando el script correspondiente.

## Uso

1. **Configuración inicial:**
   - Asegúrate de tener Python instalado en tu sistema.
   - Descarga el proyecto SoccerPredict y Scrapping desde el repositorio de GitHub.

2. **Preparación de datos:**
   - Abre el archivo principal del script en tu entorno de desarrollo (por ejemplo, Jupyter Notebook, PyCharm, etc.).
   - Asegúrate de tener instaladas las bibliotecas necesarias, como `requests`, `beautifulsoup4`, `pandas`, `ipywidgets` y `IPython`.
   - Importa las bibliotecas y las clases/funciones necesarias definidas en el script principal.

3. **Configuración de parámetros:**
   - Define la lista `year_seasons` con los años de las temporadas deseadas de las que quieres obtener datos.
   - Ingresa el nombre del equipo que deseas analizar cuando se te solicite.

4. **Ejecución del script:**
   - Ejecuta el script para iniciar el proceso de recopilación de datos.
   - El script realizará web scraping desde varias fuentes para obtener estadísticas detalladas del equipo especificado en cada temporada.
   - Los datos recopilados se guardarán en archivos CSV correspondientes a cada temporada y tipo de datos (partidos, jugadores, etc.).

5. **Análisis y uso de los datos:**
   - Una vez que se haya completado la ejecución del script, puedes utilizar los archivos CSV generados para análisis, visualizaciones u otras tareas relacionadas con los datos de fútbol recopilados.
   - Puedes cargar los archivos CSV en herramientas como Excel, pandas u otras bibliotecas de manipulación de datos para explorar y trabajar con los datos recopilados.

Ten en cuenta que el script proporcionado es un punto de partida para recopilar datos de equipos de fútbol y puedes personalizarlo según tus necesidades específicas.
