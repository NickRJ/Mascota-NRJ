using System;

namespace MascotaApp
{
    public class Mascota
    {
        public string Nombre;
        public int Edad;
        public string Tipo;
        public string Sonido;

        // Estados del Tamagotchi
        private int Hambre;      // 0 = lleno, 100 = hambriento
        private int Energia;     // 0 = cansado, 100 = lleno de energía
        private int Felicidad;   // 0 = triste, 100 = feliz
        private bool Vivo;

        public Mascota(string nombre, int edad, string tipo, string sonido)
        {
            Nombre = nombre;
            Edad = edad;
            Tipo = tipo;
            Sonido = sonido;
            Hambre = 50;
            Energia = 50;
            Felicidad = 50;
            Vivo = true;
        }

        public void EmitirSonido()
        {
            if (Vivo)
                Console.WriteLine($"{Nombre} dice: {Sonido}!");
            else
                Console.WriteLine($"{Nombre} ya no puede hacer sonidos... está muerto.");
        }

        public void Comer()
        {
            if (!Vivo) { MascotaMuerta(); return; }
            Hambre -= 20;
            Felicidad += 5;
            Energia += 5;
            NormalizarValores();
            Console.WriteLine($"{Nombre} ha comido y ahora está más feliz.");
        }

        public void Dormir()
        {
            if (!Vivo) { MascotaMuerta(); return; }
            Energia += 30;
            Hambre += 10;
            NormalizarValores();
            Console.WriteLine($"{Nombre} ha dormido y recuperó energía.");
        }

        public void Jugar()
        {
            if (!Vivo) { MascotaMuerta(); return; }
            Felicidad += 20;
            Energia -= 15;
            Hambre += 15;
            NormalizarValores();
            Console.WriteLine($"{Nombre} jugó contigo y está feliz.");
        }

        public void PasarTiempo()
        {
            if (!Vivo) return;
            Hambre += 5;
            Energia -= 5;
            Felicidad -= 5;
            RevisarVida();
        }

        private void RevisarVida()
        {
            if (Hambre >= 100 || Energia <= 0 || Felicidad <= 0)
            {
                Vivo = false;
                Console.WriteLine($"\n😢 {Nombre} ha muerto...");
            }
        }

        private void NormalizarValores()
        {
            Hambre = Math.Clamp(Hambre, 0, 100);
            Energia = Math.Clamp(Energia, 0, 100);
            Felicidad = Math.Clamp(Felicidad, 0, 100);
        }

        private void MascotaMuerta()
        {
            Console.WriteLine($"⚰️ {Nombre} ya está muerto. No puedes interactuar más.");
        }

        public void MostrarEstado()
        {
            Console.WriteLine($"\nEstado de {Nombre}:");
            Console.WriteLine($"Edad: {Edad}");
            Console.WriteLine($"Tipo: {Tipo}");
            Console.WriteLine($"Hambre: {Hambre}/100");
            Console.WriteLine($"Energía: {Energia}/100");
            Console.WriteLine($"Felicidad: {Felicidad}/100");
            Console.WriteLine($"¿Vivo?: {(Vivo ? "Sí" : "No")}");
        }
    }

    internal class Program
    {
        public static void Main(string[] args)
        {
            Mascota mascota = new Mascota("Firulais", 2, "Perro", "Guau");

            int opcion;
            do
            {
                mascota.MostrarEstado();
                Console.WriteLine("\n--- Menú Tamagotchi ---");
                Console.WriteLine("1. Dar de comer");
                Console.WriteLine("2. Jugar");
                Console.WriteLine("3. Dormir");
                Console.WriteLine("4. Escuchar sonido");
                Console.WriteLine("5. Pasar tiempo");
                Console.WriteLine("0. Salir");
                Console.Write("Elige una opción: ");

                if (!int.TryParse(Console.ReadLine(), out opcion))
                {
                    opcion = -1;
                }

                Console.Clear();

                switch (opcion)
                {
                    case 1: mascota.Comer(); break;
                    case 2: mascota.Jugar(); break;
                    case 3: mascota.Dormir(); break;
                    case 4: mascota.EmitirSonido(); break;
                    case 5: mascota.PasarTiempo(); break;
                    case 0: Console.WriteLine("Saliendo del juego..."); break;
                    default: Console.WriteLine("Opción no válida."); break;
                }

                Console.WriteLine("\nPresiona una tecla para continuar...");
                Console.ReadKey();
                Console.Clear();

            } while (opcion != 0);
        }
    }
}
