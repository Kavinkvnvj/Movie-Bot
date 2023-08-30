# Movie-Bot
import logging
from telegram import Update
from telegram.ext import Updater, CommandHandler, MessageHandler, Filters, CallbackContext

# Set your bot token here
TOKEN = 'YOUR_BOT_TOKEN'

def start(update: Update, context: CallbackContext) -> None:
    update.message.reply_text("Welcome to Movie Request Bot!")

def request_movie(update: Update, context: CallbackContext) -> None:
    movie_name = update.message.text[9:]  # Extract movie name from message
    # Here, you can add logic to search for the movie and get the download link
    download_link = "DIRECT_DOWNLOAD_LINK"
    update.message.reply_text(f"Here's the download link for '{movie_name}':\n{download_link}")

def main():
    updater = Updater(token=TOKEN, use_context=True)
    dispatcher = updater.dispatcher

    # Handlers
    dispatcher.add_handler(CommandHandler("start", start))
    dispatcher.add_handler(MessageHandler(Filters.regex(r'^/request'), request_movie))

    updater.start_polling()
    updater.idle()

if __name__ == '__main__':
    main()
