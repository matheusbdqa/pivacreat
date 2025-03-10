from datetime import datetime

class SistemaPonto:
    def __init__(self):
        self.horario_chegada = None
        self.horario_saida = None

    def registrar_chegada(self):
        self.horario_chegada = datetime.now()
        print(f"Horário de chegada registrado: {self.horario_chegada.strftime('%Y-%m-%d %H:%M:%S')}")

    def registrar_saida(self):
        if self.horario_chegada is None:
            print("Por favor, registre o horário de chegada primeiro.")
            return

        self.horario_saida = datetime.now()
        print(f"Horário de saída registrado: {self.horario_saida.strftime('%Y-%m-%d %H:%M:%S')}")

        self.calcular_duracao()

    def calcular_duracao(self):
        if self.horario_chegada and self.horario_saida:
            duracao = self.horario_saida - self.horario_chegada
            horas, remainder = divmod(duracao.seconds, 3600)
            minutos, segundos = divmod(remainder, 60)
            print(f"Duração do turno: {horas} horas, {minutos} minutos e {segundos} segundos.")
        else:
            print("Horários de chegada e/ou saída não registrados.")

    def notificar(self):
        if self.horario_chegada:
            print(f"Notificação: Você chegou às {self.horario_chegada.strftime('%H:%M:%S')}")
        if self.horario_saida:
            print(f"Notificação: Você saiu às {self.horario_saida.strftime('%H:%M:%S')}")
        if self.horario_chegada and self.horario_saida:
            self.calcular_duracao()

# Exemplo de uso
sistema = SistemaPonto()
sistema.registrar_chegada()
# Simula um tempo de trabalho
import time
time.sleep(5)  # Espera 5 segundos
sistema.registrar_saida()
sistema.notificar()
