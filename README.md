prueba-vivelab
==============

Esta es la prueba realizada

using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace SUMA_ROMANOS
{
    public partial class Form1 : Form
    {
        int valor1 = 0, valor2 = 0, suma=0;
        String valor3;
        public Form1()
        {
            InitializeComponent();
        }

        private void SUMA_Click(object sender, EventArgs e)
        {   valor1= conversion(rom1.Text);
            valor2= conversion(rom2.Text);
            if ((valor1 <= 3000) && (valor2 <= 3000))
            {
                num1.Text = Convert.ToString(valor1);
                num2.Text = Convert.ToString(valor2);
                suma = valor1 + valor2;
                rta2.Text = Convert.ToString(suma);
                valor3 = conversionarom(suma);
                rta1.Text = valor3;
                if ((valor1 == 0) || (valor2 == 0))
                {
                    MessageBox.Show("Datos de entrada incorrectos", "CALCULADORA ROMANOS", MessageBoxButtons.OK, MessageBoxIcon.Error);
                    num1.Text = "####"; num2.Text = "####"; rom1.Text = "";
                    rta1.Text = "####"; rta2.Text = "####"; rom2.Text = "";
                }
            }
            else MessageBox.Show("El rango de los valores de ingreso es de (0-3000)", "CALCULADORA ROMANOS", MessageBoxButtons.OK, MessageBoxIcon.Exclamation);
        }
        public int conversion (string romano)
        {
            int []num_Arabig;
            num_Arabig = new int[20];
            int suma = 0;
            for (int x = 0; x < 20; x++)
                num_Arabig[x] = 0;
            for (int y = 0; y < romano.Length; y++) {
                switch(romano[y])
                {
                    case 'I': num_Arabig[y] = 1; break;
                    case 'V': num_Arabig[y] = 5; break;
                    case 'X': num_Arabig[y] = 10; break;
                    case 'L': num_Arabig[y] = 50; break;
                    case 'C': num_Arabig[y] = 100; break;
                    case 'D': num_Arabig[y] = 500; break;
                    case 'M': num_Arabig[y] = 1000; break;
                    default:
                    {   return (0); break; }
                }    
            }
            for (int y = 0; y < romano.Length; y++)
            {
                if (num_Arabig[y] < num_Arabig[y + 1]) suma -= num_Arabig[y];
                else suma += num_Arabig[y];
            }
            return suma;
        }
        public String conversionarom(int numero)
        {
            String[] unidad = { "", "I", "II", "III", "IV", "V", "VI", "VII", "VIII", "IX" };
            String[] decena = { "", "X", "XX", "XXX", "XL", "L", "LX", "LXX", "LXXX", "XC" };
            String[] centena = { "", "C", "CC", "CCC", "CD", "D", "DC", "DCC", "DCCC", "CM" };
            String[] unidadmil = { "", "M", "MM", "MMM", "ĪV̄", "V̄", "V̄Ī" };
            int m = numero / 1000;
            int c = (numero - (m*1000))/100;
            int d = (numero - (m * 1000 + c*100)) / 10;
            int u = numero - (m * 1000 + c * 100 + d*10);
            if (numero >= 1000) { return unidadmil[m] + centena[c] + decena[d] + unidad[u];}
            else if (numero >= 100) { return centena[c] + decena[d] + unidad[u]; }
            else if (numero >= 10) { return decena[d] + unidad[u];}
            else { return unidad[u]; }
        }
        private void Form1_Load(object sender, EventArgs e)
        {
            rom1.CharacterCasing = CharacterCasing.Upper;
            rom2.CharacterCasing = CharacterCasing.Upper;
        }
        private void num1_Click(object sender, EventArgs e) { }
        private void rom1_TextChanged(object sender, EventArgs e) { }
        private void rom1_Click(object sender, EventArgs e) { }
        private void label1_Click(object sender, EventArgs e) { }
    }
}
