import random
from colorama import Fore, Back

class Campo():
    def __init__(self):
        self.campo = []
        self.campo_para_usuario = []
        self.tamanho = ''
        self.alfabeto = ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z']
        self.linha = 0
        self.coluna = ''
        self.ferramenta = ''
        self.vezes = 0

    def definir_dificuldade(self):
        print('Proporções\nFácil - | 10 X 10 |\nMédio - | 18 X 18 |\nDifícil - | 24 X 24 |')
        while True:
            self.tamanho = input('Escolha uma proporção (F/M/D):').upper()
            if self.tamanho != 'F' and self.tamanho != 'M' and self.tamanho != 'D':
                print('Selecione uma opção disponível.')
                continue
            break

    def cria_proporcao_do_campo(self):
        if self.tamanho == 'F':
            self.proporcao = 10
        if self.tamanho == 'M':
            self.proporcao = 18
        if self.tamanho == 'D':
            self.proporcao = 24
        for i in range(self.proporcao):
            self.campo.append([])
            self.campo_para_usuario.append([])
            for j in range(self.proporcao):
                self.campo[i].append(' ')
                if i % 2 != 0:
                    if j % 2 == 0:
                        self.campo_para_usuario[i].append(Back.GREEN + '  ' + Back.RESET)
                    else:
                        self.campo_para_usuario[i].append(Back.LIGHTGREEN_EX + '  ' + Back.RESET)
                if i % 2 == 0:
                    if j % 2 == 0:
                        self.campo_para_usuario[i].append(Back.LIGHTGREEN_EX + '  ' + Back.RESET)
                    else:
                        self.campo_para_usuario[i].append(Back.GREEN + '  ' + Back.RESET)

    def solicitar_posicao(self):
        '''Solicita linha e coluna para jogador'''
        self.linha = 0
        self.coluna = ''
        self.ferramenta = ''
        if self.vezes != 0:
            while self.ferramenta not in ['P', 'B']:
                self.ferramenta = input('Digite qual ferramenta quer utilizar(P/B): ').upper()
                if self.ferramenta != 'P' or self.ferramenta != 'B':
                    print('Digite uma ferramenta válida.')
        while self.coluna not in self.alfabeto[0:len(self.campo[0])]:
            self.coluna = input('Digite a coluna: ').upper()
            if self.coluna not in self.alfabeto[0:len(self.campo[0])]:
                print('Digite uma coluna válida.')
        while self.linha < 1 or self.linha > len(self.campo[0]):
            try:
                self.linha = int(input('Digite a linha: '))
                if self.linha < 1 or self.linha > len(self.campo[0]):
                    print('Digite uma linha válida.')
            except ValueError:
                print('Digite uma linha válida.')

    def campo_versao_inicial_dificil(self):
        # Canto inferior esquerda 
        if (self.linha == 23 or self.linha == 22 or self.linha == 21 or self.linha == 20) and (self.coluna == 0 or self.coluna == 1 or self.coluna == 2 or self.coluna == 3):
            for i in range(self.linha-4, self.linha+1):
                for j in range(5):
                    self.campo[i][j] = '0'
        # Canto inferior direita
        elif (self.linha == 23 or self.linha == 22 or self.linha == 21 or self.linha == 20) and (self.coluna == 23 or self.coluna == 22 or self.coluna == 21 or self.coluna == 20):
            for i in range(self.linha-4, self.linha+1):
                for j in range(self.coluna-4, self.coluna+1):
                    self.campo[i][j] = '0'
        # Canto superior esquerda
        elif self.coluna == 0:
            for i in range(self.linha, self.linha+5):
                for j in range(5):
                    self.campo[i][j] = '0'
        # Canto superior direita
        elif self.coluna == 23 or self.coluna == 22 or self.coluna == 21:
            for i in range(self.linha, self.linha+5):
                for j in range(self.coluna-4, self.coluna+1):
                    self.campo[i][j] = '0'
        # Borda superior
        elif self.linha == 0 and self.coluna != 0 and self.coluna != 23:
            for i in range(self.linha, self.linha+5):
                for j in range(self.coluna-1, self.coluna+4):
                    self.campo[i][j] = '0'
        # Borda inferior
        elif self.linha == 23 and self.coluna != 0 and self.coluna != 23:
            for i in range(self.linha-4, self.linha+1):
                for j in range(self.coluna-1, self.coluna+4):
                    self.campo[i][j] = '0'
        # No meio
        else:
            for i in range(self.linha-1, self.linha+4):
                for j in range(self.coluna-1, self.coluna+4):
                    self.campo[i][j] = '0'

    def campo_versao_inicial_medio(self):
        # Canto inferior esquerda
        if (self.linha == 17 or self.linha == 16 or self.linha == 15) and (self.coluna == 0 or self.coluna == 1 or self.coluna == 2):
            for i in range(self.linha-3, self.linha+1):
                for j in range(4):
                    self.campo[i][j] = '0'
        # Canto inferior direita
        elif (self.linha == 17 or self.linha == 16 or self.linha == 15) and (self.coluna == 17 or self.coluna == 16 or self.coluna == 15):
            for i in range(self.linha-3, self.linha+1):
                for j in range(self.coluna-3, self.coluna+1):
                    self.campo[i][j] = '0'
        # Canto superior esquerda
        elif self.coluna == 0:
            for i in range(self.linha, self.linha+4):
                for j in range(4):
                    self.campo[i][j] = '0'
        # Canto superior direita
        elif self.coluna == 17 or self.coluna == 16 or self.coluna == 15:
            for i in range(self.linha, self.linha+4):
                for j in range(self.coluna-3, self.coluna+1):
                    self.campo[i][j] = '0'
        # Borda superior
        elif self.linha == 0 and self.coluna != 0 and self.coluna != 17:
            for i in range(self.linha, self.linha+4):
                for j in range(self.coluna-1, self.coluna+3):
                    self.campo[i][j] = '0'
        # Borda superior
        elif self.linha == 17 and self.coluna != 0 and self.coluna != 17:
            for i in range(self.linha-3, self.linha+1):
                for j in range(self.coluna-1, self.coluna+3):
                    self.campo[i][j] = '0'
        # No meio
        else:
            for i in range(self.linha-1, self.linha+3):
                for j in range(self.coluna-1, self.coluna+3):
                    self.campo[i][j] = '0'

    def campo_versao_inicial_facil(self):
        # Canto inferior esquerda
        if (self.linha == 9 or self.linha == 8) and (self.coluna == 0 or self.coluna == 1):
            for i in range(self.linha-3, self.linha+1):
                for j in range(4):
                    self.campo[i][j] = '0'
        # Canto inferior direita
        elif (self.linha == 9 or self.linha == 8) and (self.coluna == 9 or self.coluna == 8):
            for i in range(self.linha-3, self.linha+1):
                for j in range(self.coluna-3, self.coluna+1):
                    self.campo[i][j] = '0'
        # Canto superior esquerda
        if self.coluna == 0:
            for i in range(self.linha, self.linha+3):
                for j in range(3):
                    self.campo[i][j] = '0'
        # Canto superior direita
        elif self.coluna == 9 or self.coluna == 8:
            for i in range(self.linha, self.linha+3):
                for j in range(self.coluna-2, self.coluna+1):
                    self.campo[i][j] = '0'
        # Borda superior
        elif self.linha == 0 and self.coluna != 0 and self.coluna != 9:
            for i in range(self.linha, self.linha+3):
                for j in range(self.coluna-1, self.coluna+2):
                    self.campo[i][j] = '0'
        # Borda inferior
        elif self.linha == 9 and self.coluna != 0 and self.coluna != 9:
            for i in range(self.linha-2, self.linha+1):
                for j in range(self.coluna-1, self.coluna+2):
                    self.campo[i][j] = '0'
        # No meio
        else:
            for i in range(self.linha-1, self.linha+2):
                for j in range(self.coluna-1, self.coluna+2):
                    self.campo[i][j] = '0'

    def campo_versao_inicial(self):
        self.coluna = self.alfabeto.index(self.coluna)
        self.linha -= 1
        if self.tamanho == 'F':
            self.campo_versao_inicial_facil()
        if self.tamanho == 'M':
            self.campo_versao_inicial_medio()
        if self.tamanho == 'D':
            self.campo_versao_inicial_dificil()
          
    def efeito_cascata(self):
        # Lista de posições a serem verificadas
        fila = [(self.linha, self.coluna)]
        while fila:
            lin, col = fila.pop(0)
            # Pula se já foi revelado
            if self.campo[lin][col] != ' ':
                continue
            # Se for '0', adiciona vizinhos à fila
            if self.campo[lin][col] == '0':
                for dl in [-1, 0, 1]:
                    for dc in [-1, 0, 1]:
                        nl, nc = lin + dl, col + dc
                        if 0 <= nl < self.proporcao and 0 <= nc < self.proporcao:
                            if self.campo[nl][nc] == ' ':
                                fila.append((nl, nc))

    def identificador_de_bombas(self):
        for i in range(self.proporcao):
            for j in range(self.proporcao):
                if self.campo[i][j] != ' ' and self.campo[i][j] != '0':
                    continue
                bombas = 0
                # Verifica as 8 posições ao redor
                for linha in [i - 1, i, i + 1]:
                    for coluna in [j - 1, j, j + 1]:
                        # Pula a própria célula
                        if linha == i and coluna == j:
                            continue
                        # Checa limites do campo
                        if 0 <= linha < self.proporcao and 0 <= coluna < self.proporcao:
                            if self.campo[linha][coluna] == '*':  # bomba
                                bombas += 1
                # Atualiza a célula com o número de bombas ao redor
                if bombas > 0:
                    self.campo[i][j] = str(bombas)

    def posicionar_bombas(self):
        if self.tamanho == 'F':
            total_bombas = 20
        elif self.tamanho == 'M':
            total_bombas = 40
        elif self.tamanho == 'D':
            total_bombas = 99
        bombas_colocadas = 0
        while bombas_colocadas < total_bombas:
            i = random.randint(0, self.proporcao - 1)
            j = random.randint(0, self.proporcao - 1)
            if self.campo[i][j] == ' ':
                self.campo[i][j] = '*'
                bombas_colocadas += 1
    
# Área para exibição
    def personalizacao_cores_campo_para_usuario(self):
        for i in range(self.proporcao):
            for j in range(self.proporcao):
                # Cor de onde já foi cavado
                if self.campo[i][j] == '0':
                    self.campo_para_usuario[i][j] = Back.YELLOW + '  ' + Back.RESET

    def exibir_campo_para_usuario(self):
        print('CAMPO PARA USUÁRIO')
        # Alfabeto para colunas
        for i in range(len(self.campo_para_usuario)):
            if self.alfabeto.index(self.alfabeto[i]) == 0:
                print(Fore.BLUE + '',self.alfabeto[i], end=' ' + Fore.RESET)
            elif self.alfabeto.index(self.alfabeto[i]) == len(self.campo_para_usuario)-1:
                print(Fore.BLUE + self.alfabeto[i] + Fore.RESET)
            else:
                print(Fore.BLUE + self.alfabeto[i], end=' ' + Fore.RESET)
        # Campo colorido e númeração de linhas
        aux = len(self.campo_para_usuario)
        for n, i in enumerate(self.campo_para_usuario):
            for j in range(aux):
                if j == aux-1:
                    print(i[j],Fore.BLUE +  f'{n+1}' + Fore.RESET)
                else:
                    print(i[j], end='')

    def exibir_campo_oculto(self):
        print('CAMPO OCULTO')
        for i in range(len(self.campo)):
            if self.alfabeto.index(self.alfabeto[i]) == len(self.campo)-1:
                print(' ', self.alfabeto[i])
            else:
                print(' ', self.alfabeto[i], end='  ')
        for n, i in enumerate(self.campo):
            print(i, n+1)

campo = Campo()
campo.definir_dificuldade()
campo.cria_proporcao_do_campo()

campo.exibir_campo_para_usuario()
campo.exibir_campo_oculto()
  
campo.solicitar_posicao()
campo.campo_versao_inicial()

campo.exibir_campo_para_usuario()
campo.exibir_campo_oculto()

campo.posicionar_bombas()
campo.identificador_de_bombas()
campo.efeito_cascata()

campo.personalizacao_cores_campo_para_usuario()
campo.exibir_campo_para_usuario()
campo.exibir_campo_oculto()
