# Verificar-Rut

import java.util.Scanner;

public class VerificarRut {
    public static void main(String[] args) {
        calculoDigitoVerificador();
    }

    public static void calculoDigitoVerificador() {
        int numeroRut = ingresarRut();
        String palabraRut = tomarNumeros(numeroRut);
        String palabraRutInvertida = invertirOrden(palabraRut);
        int[] arregloRut = multiplicarDigitos(palabraRutInvertida);
        int sumaRut = sumarMultiplicaciones(arregloRut);
        double dividirRut = dividirResultados(sumaRut);
        int multiplicacionEntera = tomarDecimales(dividirRut);
        int restaRut = restarResultados(sumaRut,multiplicacionEntera);
        String digitoVer = obtenerDigitoVerificador(restaRut);
        mostrarResultados(digitoVer);
    }

    public static int ingresarRut() {
        int rut;
        Scanner teclado = new Scanner(System.in);
        do {
            try {
                System.out.println("Ingrese rut: ");
                rut = teclado.nextInt();
                break;
            }catch(Exception e) {
                System.out.println("Ingrese un rut válido");
                teclado.nextLine();
            }
        }while(true);

        return (rut);
    }

    public static String tomarNumeros(int rut) {
        String cadenaRut = String.valueOf(rut);
        cadenaRut = cadenaRut.substring(0,cadenaRut.length()-1);
        return cadenaRut;
    }

    public static String invertirOrden(String cadenaRut) {
        StringBuilder stringBuilder = new StringBuilder(cadenaRut);
        return stringBuilder.reverse().toString();
    }

    public static int[] multiplicarDigitos(String cadenaRutInvertida) {
        int[] arregloCaracteres = new int[cadenaRutInvertida.length()];
        for (int i = 0; i < arregloCaracteres.length; i++) {
            arregloCaracteres[i] = Integer.parseInt(String.valueOf(cadenaRutInvertida.charAt(i)));
        }
        int[] cadena = {2,3,4,5,6,7};
        int contador = 0;
        for (int i = 0; i < arregloCaracteres.length; i++) {
            if(contador == cadena.length){
                contador = 0;
                arregloCaracteres[i] *= cadena[contador];
                contador++;
            }else{
                arregloCaracteres[i] *= cadena[contador];
                contador++;
            }
        }
        return arregloCaracteres;
    }

    public static int sumarMultiplicaciones(int[] arregloCaracteres) {
        int sumaArregloRut = 0;
        for (int i = 0; i < arregloCaracteres.length; i++) {
            sumaArregloRut += arregloCaracteres[i];
        }
        return sumaArregloRut;
    }

    public static double dividirResultados(int sumaArregloRut) {
        return sumaArregloRut/11;
    }

    public static int tomarDecimales(double divisionSumas) {
        return ((int)divisionSumas)*11;
    }

    public static int restarResultados(int sumaMultiplicaciones, int multSinDecimales) {
        return Math.abs(sumaMultiplicaciones - multSinDecimales);
    }

    public static String obtenerDigitoVerificador(int restaNumeros) {
        String resultadoDigito = String.valueOf(11 - restaNumeros);
        if(resultadoDigito.equals("10")){
            resultadoDigito = "k";
        }else if(resultadoDigito.equals("11")){
            resultadoDigito = "0";
        }
        return resultadoDigito;
    }

    public static void mostrarResultados(String resultadoDigito) {
        System.out.println("El dígito verificador es: "+resultadoDigito);
    }
}
