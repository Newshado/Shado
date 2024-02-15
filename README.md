
from Google.cloud import messaging from twilio.twiml.messaging_response import MessagingResponse

app = Flask(__name__)

@app.route("/webhook", methods=['POST'])
def webhook():
    incoming_msg = request.values.get('Body', '').lower()
    resp = MessagingResponse()
    msg = resp.message()

    if 'hello' in incoming_msg:
        msg.body("Hi there!")
    elif 'help' in incoming_msg:
        msg.body("How can I assist you?")
    else:
        msg.body("Sorry, I didn't understand that.")

    return str(resp)

if __name__ == "__main__":
    app.run(debug=True)
