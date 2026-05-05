import gifos
from datetime import datetime

# Rutas a las fuentes (Asegúrate de que estos archivos existan en tu repo)
# Puedes usar cualquier fuente .ttf que tengas en una carpeta /fonts
FONT_FILE = "./fonts/IosevkaTermNerdFont-Bold.ttf"

def main():
    # Inicializar terminal: (Ancho, Alto, x_pad, y_pad, fuente, tamaño)
    t = gifos.Terminal(700, 400, 20, 20, FONT_FILE, 14)
    t.set_fps(15)
    
    # Configurar el Prompt
    t.set_prompt("\x1b[0;92mgael\x1b[0m@\x1b[0;94mgithub ~> \x1b[0m")
    t.gen_prompt(1)
    
    # 1. Animación de escritura inicial
    t.gen_typing_text("Gael comenzo...", 1, contin=True)
    t.clone_frame(15)
    
    # 2. Empezar a escribir código
    t.gen_prompt(3)
    t.gen_typing_text("python3 initialize_project.py", 3, contin=True)
    t.clone_frame(5)
    
    # 3. Animación de carga con círculo y barra
    t.gen_text("Cargando modulos del sistema...", 5)
    
    spinner = ['◐', '◓', '◑', '◒']
    pasos = 20
    for i in range(pasos + 1):
        porcentaje = (i * 100) // pasos
        llenado = i // 2
        barra = "█" * llenado + "░" * (10 - llenado)
        char_circulo = spinner[i % 4]
        
        # Actualizar la misma línea para efecto de animación
        t.delete_row(7)
        t.gen_text(f"\x1b[93m{char_circulo}\x1b[0m Progreso: [{barra}] {porcentaje}%", 7)
        t.clone_frame(2)

    # 4. Mensaje final
    t.gen_text("\x1b[96m[OK] Gael ha iniciado la sesion correctamente.\x1b[0m", 9)
    t.gen_prompt(11)
    
    # Mantener el cuadro final unos segundos
    t.clone_frame(60)
    
    # Guardar como GIF
    t.gen_gif()

if __name__ == "__main__":
    main()
