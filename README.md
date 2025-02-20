# ProjectBot

This repository contains a python script running a Discord bot that fetches information from messages in forum channels and creates corresponding entries in a Notion database. It's designed to help with project management, allowing users to quickly transfer and track project details from Discord discussions to a structured Notion database.

## Prerequisites
Before you begin, ensure you have the following:

- Anaconda or Miniconda installed on your system. You can download Anaconda [here](https://www.anaconda.com/products/individual) or Miniconda [here](https://docs.conda.io/en/latest/miniconda.html).
- A Discord bot token. Follow the instructions [here](https://discordpy.readthedocs.io/en/latest/discord.html) to create a bot and obtain your token.
- A Notion integration token and a database ID. Follow the setup instructions [here](https://developers.notion.com/docs/getting-started) to create an integration and share a database with it.
- An Airtable API key and base ID. Set up an Airtable account and create a new base for the bot to interact with.
- A Heroku account for deployment.

# Setup
1. **Clone the Repository**

Clone this repository to your local machine using:

```sh
git clone <repository-url>
cd <repository-directory>
```

2. **Create Conda Environment**

Create a new Conda environment using the environment.yml file included in the project:

```sh
conda env create -f environment.yml
```

This will create a new environment named projectbot with all the necessary Python dependencies installed.

3. **Activate the Environment**

Activate the newly created Conda environment:

```sh
conda activate projectbot
```

4. **Configure Secrets**

Create a secrets.yml file in the project directory with your Discord bot token and Notion integration details:

```yaml
discord_bot_token: "YOUR_DISCORD_BOT_TOKEN"
notion_integration_token: "YOUR_NOTION_INTEGRATION_TOKEN"
notion_database_id: "YOUR_NOTION_DATABASE_ID"
airtable_api_key: "YOUR_AIRTABLE_API_KEY"
```

Make sure to replace the placeholders with your actual tokens and IDs.

## Running the Bot Locally
1. **Start the Bot**

With the Conda environment activated and the secrets configured, start the bot by running:

```sh
python bot.py
```


2. **Using the Bot**

- In any Discord server where the bot is a member, navigate to a forum channel or a thread and type !track to trigger the bot. The bot will fetch information from the original post in the thread and create a corresponding entry in your Notion database.
- Use the !projects and !tasks commands to generate shortlists of important projects and tasks.

## Deployment
To deploy the bot on Heroku, follow these steps:

1. Install the Heroku CLI by following the instructions here.
2. Log in to your Heroku account using the CLI:

```sh
heroku login
```
3. Create a new Heroku app:
```sh
heroku create <app-name>
```
4. Set the environment variables on Heroku using the secrets from your secrets.yml file:
```sh
heroku config:set DISCORD_BOT_TOKEN=YOUR_DISCORD_BOT_TOKEN
heroku config:set NOTION_INTEGRATION_TOKEN=YOUR_NOTION_INTEGRATION_TOKEN
heroku config:set NOTION_DATABASE_ID=YOUR_NOTION_DATABASE_ID
heroku config:set AIRTABLE_API_KEY=YOUR_AIRTABLE_API_KEY
heroku config:set AIRTABLE_BASE_ID=YOUR_AIRTABLE_BASE_ID
```
5. Push the code to Heroku:
```sh
git push heroku main
```
6. Start the bot on Heroku:
```sh
heroku ps:scale worker=1
```
Your bot should now be running on Heroku.

## Notes
- Ensure the bot has the necessary permissions on your Discord server to read messages and access forum channels.
- The Notion database must be shared with your Notion integration for the bot to create entries.
- Make sure to set up the appropriate tables and fields in your Airtable base to match the bot's functionality.