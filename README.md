# bottelegramm
   from flask import Flask, request
   import requests

   app = Flask(__name__)

   TELEGRAM_BOT_TOKEN = '8365590466:AAH6DsNH6XtuvZuMqPeXeZsFkNEl1Ohwwtk'
   CHAT_ID = '7935869247'

   @app.route('/webhook', methods=['POST'])
   def webhook():
       data = request.json
       # Обработка данных от GitHub
       if 'commits' in data:
           for commit in data['commits']:
               message = f"Новый коммит в репозитории: {commit['message']}"
               send_telegram_message(message)
       return '', 200

   def send_telegram_message(message):
       url = f'https://api.telegram.org/bot{8365590466:AAH6DsNH6XtuvZuMqPeXeZsFkNEl1Ohwwtk}/sendMessage'
       payload = {
           'chat_id': CHAT_ID,
           'text': message
       }
       requests.post(url, json=payload)

   if __name__ == '__main__':
       app.run(port=5000)
   
