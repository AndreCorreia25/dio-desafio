# dio-desafio
desafio de projetogithub

# Codigo de um Jogo da velha realizado em python

class Jogodavelha:
  def __init__(self):
    self.tabuleiro = [' '] * 9 
    self.jogadores = ['X', 'O']
    self.jogador_atual = self.jogadores[0]

  def verificar_jogada(self, posicao):
    if self.tabuleiro[posicao] == ' ':
      self.tabuleiro[posicao] = self.jogador_atual
      return True
    else:
      return False

  def verificar_vencedor(self):
    possibilidades_vitoria = [
        [0,1,2], [3,4,5],[6,7,8],
        [0,3,6],[1,4,7],[2,5,8],
        [0,4,8],[2,4,6]
    ]    

    for p in possibilidades_vitoria:
      if self.tabuleiro[p[0]] == self.tabuleiro[p[1]] == self.tabuleiro[p[2]] != ' ':
        return self.tabuleiro[p[0]]

    if ' ' not in self.tabuleiro:
        return 'Empate'

    return None

  def imprimir_tabuleiro(self):
    for i in range (0, 9, 3):
      print(self.tabuleiro[i], '|', self.tabuleiro[i+1], '|', self.tabuleiro[i+2])
      if i != 6:
        print('--+---+--')

  def jogar(self):
    jogar_novamente = True
    while jogar_novamente:
      self.tabuleiro = [' '] * 9
      self.jogador_atual = self.jogadores[0]
      while True:
        print('Jogador', self.jogador_atual)
        posicao = int(input('Digite a posição (0-8): '))

        if posicao < 0 or posicao > 8:
          print('Posição inválida. Tente novamente.')
          continue

        if not self.verificar_jogada(posicao):
          print('Posição já ocupada. Tente novamente.')
          continue

        self.imprimir_tabuleiro()

        vencedor = self.verificar_vencedor()

        if vencedor:
          print('Jogador', vencedor, 'venceu!')
          break

        if vencedor == 'Empate':
          print('Empate!')
          break

        self.jogador_atual = self.jogadores[1] if self.jogador_atual == self.jogadores[0] else self.jogadores[0]

      jogar_novamente = input('Deseja jogar novamente? (S/N)').lower() == 's'
    
    print("Obrigado por jogar! Até a próxima!")
    
jogo = Jogodavelha()
jogo.jogar()
