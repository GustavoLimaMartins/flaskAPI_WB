from flask import Flask, request, jsonify

app = Flask(__name__)

# URL de verificação do Webhook (para validação)
@app.route('/webhook', methods=['GET'])
def verify_webhook():
    # Verificação com o Facebook (token fornecido por você)
    verify_token = "YOUR_VERIFY_TOKEN"  # Substitua pelo seu token de verificação
    challenge = request.args.get('hub.challenge')
    mode = request.args.get('hub.mode')
    token = request.args.get('hub.verify_token')

    if mode == 'subscribe' and token == verify_token:
        return challenge, 200
    else:
        return "Verification failed", 403

# Processar o evento quando uma mensagem é recebida
@app.route('/webhook', methods=['POST'])
def handle_message():
    # Recebe os dados enviados pelo WhatsApp
    data = request.get_json()
    print("Dados recebidos: ", data)

    # Extraia a mensagem e o número do usuário
    try:
        message_data = data['entry'][0]['messaging'][0]
        user_phone_number = message_data['sender']['id']
        message_text = message_data['message']['text']['body']
        print(f"Mensagem recebida de {user_phone_number}: {message_text}")
    except KeyError:
        print("Erro ao processar a mensagem.")
    
    return jsonify({"status": "success"}), 200

if __name__ == '__main__':
    app.run(debug=True, port=5000)
