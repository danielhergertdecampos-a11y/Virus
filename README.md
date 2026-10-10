
import os
import time
import random
import sys
import shutil

# TITAN TIGRE DEFENDER V4
# PEGADINHA VISUAL SEGURA

VERDE = "\033[92m"
VERMELHO = "\033[91m"
AMARELO = "\033[93m"
CIANO = "\033[96m"
RESET = "\033[0m"

DURACAO = 120  # aproximadamente 2 minutos

def limpar_tela():
    print("\033[2J\033[H", end="", flush=True)

def dimensoes():
    t = shutil.get_terminal_size((40, 24))
    return t.columns, t.lines

def centralizar(texto):
    largura, _ = dimensoes()
    for linha in texto.split("\n"):
        print(linha.center(largura))

def esperar(segundos=1):
    time.sleep(segundos)

def matrix(duracao=8):
    caracteres = "0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ"
    fim = time.time() + duracao
    largura, altura = dimensoes()

    while time.time() < fim:
        limpar_tela()
        print(VERDE, end="")

        for _ in range(max(5, altura - 2)):
            linha = "".join(
                random.choice(caracteres)
                for _ in range(max(10, largura))
            )
            print(linha)

        print(RESET, end="", flush=True)
        esperar(0.18)

def barra_progresso():
    limpar_tela()
    print(CIANO)
    centralizar("INICIALIZANDO TITAN TIGRE DEFENDER")
    print()

    for i in range(41):
        largura, _ = dimensoes()
        porcentagem = int(i * 100 / 40)
        barra = "#" * i + "-" * (40 - i)

        texto = f"[{barra}] {porcentagem}%"
        sys.stdout.write("\r" + texto[:largura].ljust(largura))
        sys.stdout.flush()
        esperar(0.08)

    print(RESET)
    esperar(1)

def alerta(titulo, mensagem, cor=VERMELHO, duracao=5):
    limpar_tela()
    largura, altura = dimensoes()

    print(cor + "!" * max(10, largura))
    print()
    centralizar(titulo)
    print()
    centralizar(mensagem)
    print()

    for _ in range(max(2, altura // 5)):
        print(("! " * (largura // 2 + 1))[:largura])

    print(RESET)
    esperar(duracao)

def sequencia_alertas():
    mensagens = [
        ("ALERTA DE SEGURANCA",
         "AMEACA FICTICIA DETECTADA"),
        ("TITAN DEFENDER",
         "INICIANDO PROTOCOLO DE PROTECAO"),
        ("ACESSO SUSPEITO",
         "SIMULACAO VISUAL EM ANDAMENTO"),
        ("SISTEMA EM ALERTA",
         "ESTA TELA E UMA ANIMACAO"),
        ("VERIFICACAO VISUAL",
         "NENHUM ARQUIVO ESTA SENDO ANALISADO"),
        ("PROTOCOLO TITAN",
         "DEMONSTRACAO DE SEGURANCA"),
        ("ALERTA VERMELHO",
         "AMEACA FICTICIA - SEM RISCO REAL"),
        ("DIAGNOSTICO",
         "NENHUMA ALTERACAO FOI REALIZADA"),
    ]

    inicio = time.time()
    indice = 0

    while time.time() - inicio < DURACAO:
        titulo, mensagem = mensagens[indice % len(mensagens)]
        alerta(titulo, mensagem, VERMELHO, duracao=4)

        # Efeito Matrix entre os alertas
        matrix(duracao=3)
        indice += 1

def revelar():
    limpar_tela()
    largura, altura = dimensoes()

    print(VERDE)
    for _ in range(max(1, altura // 6)):
        centralizar("=" * min(34, largura))

    print()
    centralizar("TITAN TIGRE DEFENDER")
    centralizar("PEGADINHA! 😂")
    print()
    centralizar("VOCE CAIU NA BRINCADEIRA!")
    centralizar("TUDO ERA UMA SIMULACAO VISUAL.")
    print()
    centralizar("NENHUM VIRUS FOI CRIADO.")
    centralizar("NENHUM ARQUIVO FOI ALTERADO.")
    centralizar("SEU CELULAR NAO FOI HACKEADO.")
    print(RESET)

    input("\nPressione ENTER para sair...")

def main():
    try:
        limpar_tela()
        print(VERDE)
        centralizar("TITAN TIGRE DEFENDER")
        centralizar("VERSAO 4.0 - TELA AMPLIADA")
        centralizar("SIMULACAO VISUAL SEGURA")
        print(RESET)
        esperar(2)

        matrix(duracao=8)
        barra_progresso()
        sequencia_alertas()
        revelar()

    except KeyboardInterrupt:
        limpar_tela()
        print(RESET + "Simulacao encerrada pelo usuario.")

if __name__ == "__main__":
    main()
