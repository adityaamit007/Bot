from telegram import Update
from telegram.ext import Updater, CommandHandler, MessageHandler, Filters, CallbackContext

# Your bot token from BotFather
BOT_TOKEN = "your_bot_token_here"

# Command to start the bot
def start(update: Update, context: CallbackContext):
    update.message.reply_text(
        "Welcome to My Bot!\n"
        "Here are the available commands:\n"
        "/start - Start the bot\n"
        "/help - Get help with commands\n"
        "/info - Get bot info\n"
        "/pay - Make a payment\n"
        "Type anything else to chat!"
    )

# Command to show help
def help_command(update: Update, context: CallbackContext):
    update.message.reply_text("This bot supports the following commands:\n/start\n/help\n/info\n/pay")

# Command to show bot info
def info(update: Update, context: CallbackContext):
    update.message.reply_text("I am a bot created by you. I'm here to help!")

# Command for payment (example)
def pay(update: Update, context: CallbackContext):
    update.message.reply_text("Payment system is under development!")

# Function to handle regular messages
def handle_message(update: Update, context: CallbackContext):
    user_message = update.message.text
    update.message.reply_text(f"You said: {user_message}")

# Main function to start the bot
def main():
    updater = Updater(BOT_TOKEN, use_context=True)
    dp = updater.dispatcher

    # Add command handlers
    dp.add_handler(CommandHandler("start", start))
    dp.add_handler(CommandHandler("help", help_command))
    dp.add_handler(CommandHandler("info", info))
    dp.add_handler(CommandHandler("pay", pay))

    # Add a handler for general text messages
    dp.add_handler(MessageHandler(Filters.text & ~Filters.command, handle_message))

    # Start polling
    updater.start_polling()
    updater.idle()

if __name__ == "__main__":
    main()
