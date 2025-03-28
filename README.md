# Python-number-finder

import phonenumbers
from phonenumbers import timezone
from phonenumbers import geocoder
from phonenumbers import carrier

def obter_informacoes_telefone(numero):
    """
    Obtém informações de fuso horário, localização e operadora de um número de telefone.

    Args:
        numero: O número de telefone a ser analisado (string).
    """
    try:
        # Analisa o número de telefone
        numero_telefone = phonenumbers.parse(numero)

        # Obtém os fusos horários associados ao número
        fusos_horarios = timezone.time_zones_for_number(numero_telefone)
        print("Fuso(s) horário(s):", fusos_horarios)

        # Obtém a localização geográfica do número
        localizacao = geocoder.description_for_number(numero_telefone, "pt") # "pt" para Português
        print("Localização:", localizacao)

        # Obtém o nome da operadora do número
        operadora = carrier.name_for_number(numero_telefone, "pt") # "pt" para Português
        print("Operadora:", operadora)

    except phonenumbers.phonenumberutil.NumberParseException:
        print("Número de telefone inválido.")
    except Exception as e:
        print(f"Ocorreu um erro inesperado: {e}")

# Solicita o número de telefone ao usuário
numero_telefone = input("Digite o número de telefone com o código do país: ")

# Chama a função para obter as informações
obter_informacoes_telefone(numero_telefone)
