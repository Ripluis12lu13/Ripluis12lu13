class Floresta:
    def __init__(self):
        self.mapa = [
            ['F', 'F', 'C', 'F', 'R'],
            ['F', 'M', 'F', 'C', 'F'],
            ['R', 'F', 'T', 'F', 'F'],
            ['F', 'F', 'F', 'M', 'C'],
            ['C', 'R', 'F', 'F', 'F']
        ]
        self.posicao = (0, 0)
        self.inventario = []
        self.vida = 100

    def mostrar_mapa(self):
        for y, linha in enumerate(self.mapa):
            for x, celula in enumerate(linha):
                if (x, y) == self.posicao:
                    print("P", end=" ")  # P de Player (Jogador)
                else:
                    print(celula, end=" ")
            print()
        print()

    def mover(self, direcao):
        x, y = self.posicao
        if direcao == 'norte' and y > 0:
            self.posicao = (x, y - 1)
        elif direcao == 'sul' and y < len(self.mapa) - 1:
            self.posicao = (x, y + 1)
        elif direcao == 'leste' and x < len(self.mapa[0]) - 1:
            self.posicao = (x + 1, y)
        elif direcao == 'oeste' and x > 0:
            self.posicao = (x - 1, y)
        else:
            print("Movimento inválido. Tente novamente.")
            return
        self.mostrar_mapa()
        self.encontrar_evento()

    def encontrar_evento(self):
        evento = random.choice(["item", "criatura", "nada"])
        if evento == "item":
            self.encontrar_item()
        elif evento == "criatura":
            self.encontrar_criatura()
        else:
            print("Você não encontrou nada de interessante.")

    def encontrar_item(self):
        itens = ["chave", "poção de cura", "espada mágica", "tesouro"]
        item = random.choice(itens)
        self.inventario.append(item)
        print(f"Você encontrou um(a) {item}!")

    def encontrar_criatura(self):
        criaturas = ["fada", "elfo", "dragão", "lobo místico"]
        criatura = random.choice(criaturas)
        print(f"Você encontrou um(a) {criatura}!")
        self.batalha(criatura)

    def batalha(self, criatura):
        resultado = random.choice(["vitória", "derrota"])
        if resultado == "vitória":
            print(f"Você derrotou o(a) {criatura}!")
        else:
            dano = random.randint(10, 30)
            self.vida -= dano
            print(f"Você foi derrotado pelo(a) {criatura} e perdeu {dano} pontos de vida.")
        if self.vida <= 0:
            print("Você morreu! Fim de jogo.")
            exit()

def jogar():
    print("Bem-vindo à Aventura na Floresta Encantada!")
    floresta = Floresta()
    floresta.mostrar_mapa()

    while True:
        acao = input("O que você quer fazer? (mover, sair): ").lower()
        if acao == "mover":
            direcao = input("Para qual direção você quer se mover? (norte, sul, leste, oeste): ").lower()
            floresta.mover(direcao)
        elif acao == "sair":
            print("Saindo do jogo. Até a próxima!")
            break
        else:
            print("Ação desconhecida. Tente novamente.")

if __name__ == "__main__":
    jogar()
