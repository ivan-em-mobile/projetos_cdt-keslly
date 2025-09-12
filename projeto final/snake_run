import pygame
import random

# Inicializa o pygame
pygame.init()

# Cria a tela
tela = pygame.display.set_mode((600, 400))
pygame.display.set_caption('Game Snake Run')

# Fonte para o placar
fonte = pygame.font.SysFont('Arial', 25)

# Corpo da cobra e direção inicial
corpo_cobra = [(100, 50)]
direcao = (10, 0)

# Primeira comida
comida = (300, 200)

# Pontuação
pontuacao = 0

# Função para desenhar o fundo de grama com dois tons
def desenhar_grama():
    cor1 = (0, 180, 0)  # verde mais claro
    cor2 = (0, 140, 0)  # verde mais escuro
    tamanho = 20

    for y in range(0, 400, tamanho):
        for x in range(0, 600, tamanho):
            # alterna a cor com base na posição
            if (x // tamanho + y // tamanho) % 2 == 0:
                cor = cor1
            else:
                cor = cor2
            pygame.draw.rect(tela, cor, (x, y, tamanho, tamanho))

# Função para desenhar os elementos
def desenhar():
    desenhar_grama()

    # desenha a cobra
    for parte in corpo_cobra:
        pygame.draw.rect(tela, (0, 200, 225,), (*parte, 10, 10))

    # desenha a comida
    pygame.draw.rect(tela, (128, 0, 128), (*comida, 10, 10))

    # desenha o placar
    texto = fonte.render(f"Pontuação: {pontuacao}", True, (255, 255, 255))
    tela.blit(texto, (10, 10))

    pygame.display.update()

# Controle do jogo
rodando = True
relogio = pygame.time.Clock()

while rodando:
    for evento in pygame.event.get():
        if evento.type == pygame.QUIT:
            rodando = False

        if evento.type == pygame.KEYDOWN:
            if evento.key == pygame.K_UP and direcao != (0, 10):
                direcao = (0, -10)
            elif evento.key == pygame.K_DOWN and direcao != (0, -10):
                direcao = (0, 10)
            elif evento.key == pygame.K_LEFT and direcao != (10, 0):
                direcao = (-10, 0)
            elif evento.key == pygame.K_RIGHT and direcao != (-10, 0):
                direcao = (10, 0)

    # Nova posição da cabeça
    nova_cabeca = (corpo_cobra[0][0] + direcao[0], corpo_cobra[0][1] + direcao[1])
    corpo_cobra.insert(0, nova_cabeca)

    # Verifica se comeu a comida
    if nova_cabeca == comida:
        comida = (random.randrange(0, 59) * 10, random.randrange(0, 39) * 10)
        pontuacao += 1
    else:
        corpo_cobra.pop()

    # Verifica colisão com o corpo
    if nova_cabeca in corpo_cobra[1:]:
        rodando = False

    # Verifica colisão com a parede
    if nova_cabeca[0] < 0 or nova_cabeca[0] >= 600 or nova_cabeca[1] < 0 or nova_cabeca[1] >= 400:
        rodando = False

    desenhar()
    relogio.tick(15)

pygame.quit()
