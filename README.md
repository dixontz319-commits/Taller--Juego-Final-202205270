# Taller--Juego-Final-202205270
# Cat Hunter
Descripcion
El juego se basa en la cacería de un gato llamado mishifu, su historia inicia cuando lo contratan
para exterminar a la plaga de ratones enormes dentro de una fábrica, pero no es cosa fácil, ya que
los ratones tienen armas como cuchillos, tenedores afilados, cohetes bomba entre otras armas
Estas armas de los ratones, afectan la vida del protagonista y este solo tiene un escudo encima
para protegerse y sus únicas armas son sus garras y su cola, se la pasara en cada punto de la
fabrica cazando a sus presas y al finalizar cada este debe enfrentarse a todo n arsenal de armas
filosas y muy peligrosas

# Fase 1 Analisis

Este juego durante su trayectoria demuestra la profundidad de la soledad de un gato al querer
impresionar con sus habilidades y demostrar que es alguien con talento, ya que su antepasado
sufría de burlas de compañeros y de su misma familia, da todo por cumplir un trabajo que nadie
de los gatos se animaría a hacer. Y Demuestra como una civilización que se ha mantenido durante
mucho tiempo en una fábrica de arsenal militar puede evolucionar bastante durante un largo
tiempo.
Su calidad de juego es de únicamente de 5 botones en todos los mapas,
Uno ataca con sus garras
 X salta sus objetos y armas
O se protege con su escudo
B corre rápido
K potenciador para curar sus heridas

# Fase 2 Diagrama de Flujo
Se caracteriza en tener asegurado las etapas con las 5 estrellas ya que si no se logran le toca repetir todo al jugador, mientras mas tarde en alcanzar las estrellas de cada etapa mas tardara en jugar los demas biomas, tambien se enfoca en el lobby donde se da la instruccion de elegir si participar o sea jugar o dejar el juego, ambas opciones estan estructuradas y el eso de armas y escudo tambien estan respaldados para llevar a cabo un orden en todo 

# Fase 3 Codigo FINAL 
# THE CAT HUNTER
# Proyecto de Programación 2

nombre_gato = "Mishifu"

vida = 100
escudo = 50
atunes = 0
etapa = 1

print("====================================")
print("        THE CAT HUNTER")
print("====================================")
print("Protagonista:", nombre_gato)
print()
print("Mishifu ha sido contratado para")
print("eliminar una plaga de ratones")
print("enorme dentro de una fábrica.")
print()

input("Presiona ENTER para comenzar...")

# ==========================================
# FUNCIONES
# ==========================================

def mostrar_estado():
    print("\n----------------------------")
    print("ESTADO DE MISHIFU")
    print("----------------------------")
    print("Vida:", vida)
    print("Escudo:", escudo)
    print("Atún:", atunes)
    print("Etapa:", etapa)
    print("----------------------------")


def atacar():
    daño = random.randint(10, 25)
    print("\nMishifu ataca con sus garras.")
    print("Daño causado:", daño)
    return daño


def saltar():
    print("\nMishifu salta y esquiva el ataque.")
    print("¡El ataque enemigo fue evitado!")


def proteger():
    global escudo

    escudo += 10

    if escudo > 50:
        escudo = 50

    print("\nMishifu utiliza su escudo.")
    print("Escudo actual:", escudo)


def correr():
    print("\nMishifu corre rápidamente por la fábrica.")
    print("¡Logró alejarse del enemigo!")


def curarse():
    global vida

    recuperacion = random.randint(10, 25)
    vida += recuperacion

    if vida > 100:
        vida = 100

    print("\nMishifu encontró un potenciador.")
    print("Recuperó", recuperacion, "puntos de vida.")
    print("Vida actual:", vida)


def ataque_enemigo():
    global vida
    global escudo

    daño = random.randint(5, 20)

    if escudo > 0:
        if daño <= escudo:
            escudo -= daño
            daño_real = 0
        else:
            daño_real = daño - escudo
            escudo = 0

        print("\nEl enemigo atacó.")
        print("El escudo recibió el impacto.")

    else:
        daño_real = daño

    vida -= daño_real

    if daño_real > 0:
        print("Mishifu perdió", daño_real, "de vida.")
    else:
        print("¡El escudo protegió completamente a Mishifu!")


def batalla(enemigo, vida_enemigo):
    global vida

    print("\n====================================")
    print("        ENEMIGO APARECIÓ")
    print("====================================")
    print("Enemigo:", enemigo)
    print("Vida del enemigo:", vida_enemigo)

    while vida_enemigo > 0 and vida > 0:

        mostrar_estado()

        print("\n¿Qué quieres hacer?")
        print("1. Atacar con garras")
        print("2. Saltar")
        print("3. Protegerse con escudo")
        print("4. Correr")
        print("5. Usar potenciador")

        opcion = input("Selecciona una opción: ")

        if opcion == "1":

            daño = atacar()
            vida_enemigo -= daño

            if vida_enemigo < 0:
                vida_enemigo = 0

            print("Vida del enemigo:", vida_enemigo)

        elif opcion == "2":
            saltar()
            continue

        elif opcion == "3":
            proteger()

        elif opcion == "4":
            correr()
            continue

        elif opcion == "5":
            curarse()

        else:
            print("Opción incorrecta.")
            continue

        if vida_enemigo > 0:
            ataque_enemigo()

    if vida <= 0:
        return False

    print("\n¡Mishifu derrotó a", enemigo, "!")
    return True


# ==========================================
# HISTORIA
# ==========================================

print("\n====================================")
print("           LA FÁBRICA")
print("====================================")

print("\nMishifu entra a la fábrica.")
print("La fábrica está llena de ratones enormes.")
print("Los ratones poseen diferentes armas.")

# ==========================================
# ETAPA 1
# ==========================================

print("\n******** ETAPA 1 ********")

if not batalla("Ratón con cuchillo", 60):
    print("\nGAME OVER")
    exit()

# ==========================================
# ETAPA 2
# ==========================================

etapa = 2

print("\n******** ETAPA 2 ********")

if not batalla("Ratón con tenedor afilado", 80):
    print("\nGAME OVER")
    exit()

# ==========================================
# ETAPA 3
# ==========================================

etapa = 3

print("\n******** ETAPA 3 ********")

if not batalla("Ratón con cohete bomba", 100):
    print("\nGAME OVER")
    exit()

# ==========================================
# JEFE FINAL
# ==========================================

etapa = 4

print("\n====================================")
print("           JEFE FINAL")
print("====================================")

print("Mishifu ha llegado a la última etapa.")
print("¡Un ejército de ratones robots aparece!")

if not batalla("Ratón robot gigante", 150):
    print("\nGAME OVER")
    exit()

# ==========================================
# FINAL
# ==========================================

atunes = 20

print("\n====================================")
print("          ¡MISIÓN COMPLETADA!")
print("====================================")

print("Mishifu derrotó a todos los enemigos.")
print("Recibió", atunes, "latas de atún y pescado.")
print()
print("Después de completar su trabajo...")
print("Mishifu conoce a una gatita llamada Vanessa.")
print()
print("🐱 Mishifu: ¡Lo logré!")
print("🐱 Vanessa: ¡Estoy orgullosa de ti!")
print()
print("====================================")
print("       FIN DE THE CAT HUNTER")
print("====================================")

# Fase 4-Presentacion Final 
