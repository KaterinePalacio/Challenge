# Challenge
package juego;
import javax.swing.JOptionPane;

public class Juego {

    public Juego() {
    }
    
    public static void main(String[] args) {
        Respuesta objres;
        objres = new Respuesta();
        Pregunta objpre;
        objpre = new Pregunta();
        Archivo objarch;
        objarch = new Archivo();
        objarch.AbrirArchivoModoEscritura("C:\\Juego\\juego.txt");
        
        Pregunta[] preguntas =  {
            new Pregunta("Quién descubrió América?", new Respuesta[] {
                new Respuesta("Cristobal Colón", 'A', true),
                    new Respuesta("Hernán Cortés", 'B', false),
                    new Respuesta("El rey de Inglaterra", 'C', false),
                    new Respuesta("Ninguno de los anteriores", 'D', false)
            }),
            new Pregunta("23 + 3?", new Respuesta[] {
                new Respuesta("17", 'A', false),
                    new Respuesta("12", 'B', false),
                    new Respuesta("32", 'C', false),
                    new Respuesta("26", 'D', true)
            }),
        };

        for (Pregunta p: preguntas) {
            p.preguntar();
        }
    }
}

package juego;
import java.io.*;
import javax.swing.JOptionPane;

public class Archivo {
    
    File ArchPer;
    FileReader ArchPerLectura;
    BufferedReader BufferPer;
    FileWriter ArchPerEscritura;
    PrintWriter objImpresion;
    Juego objAlc;
    
    public String AbrirArchivoModoLectura(String ruta){
     String mensaje="¡Se abrió de modo lectura!";
     try{
     ArchPer= new File(ruta);
     ArchPerLectura = new FileReader(ArchPer);
     BufferPer = new BufferedReader(ArchPerLectura);
     }
     catch(Exception objException){
         mensaje=objException.getMessage();      
     }
     return mensaje;
    }
    
     public String CerrarArchivoModoLectura(String ruta){
     String mensaje="¡Se cerró de modo lectura!";
     try{
     BufferPer.close();
     }
     catch(Exception objException){
         mensaje=objException.getMessage();      
     }
     return mensaje;
    }
     
      public String AbrirArchivoModoEscritura(String ruta){
     String mensaje="¡Se abrió de modo escritura!";
     try{
     ArchPer= new File(ruta);
     ArchPerEscritura = new FileWriter(ArchPer, true);
     objImpresion = new PrintWriter(ArchPerEscritura);
     }
     catch(Exception objException){
         mensaje=objException.getMessage();      
     }
     return mensaje;
    }
      
       public String CerrarArchivoModoEscritura(String ruta){
     String mensaje="¡Se cerró de modo escritura!";
     try{
     
     objImpresion.close();
     }
     catch(Exception objException){
         mensaje=objException.getMessage();      
     }
     return mensaje;
    }
       
       public String[] LeerRegistro(){
        int N;
        N=Integer.parseInt("Ingrese cantidad de escuelas nuevamente");
        String Reg="",mensaje;
        String vec[];
        vec= new String[N];
        try{
        Reg=BufferPer.readLine();
        vec=Reg.split(",");
        }
        catch(Exception objException){
        mensaje=objException.getMessage();
        }
        return vec;
       }
       
       public String GrabarRegistro(String Reg){
       String mensaje="Grabar un registro";
       try{
       objImpresion.print(Reg);
       objImpresion.println();
       }
       catch(Exception objException) {
           mensaje=objException.getMessage();
       }
       return mensaje;
       }
       
       public void Reinicio(String ruta){
       try{
         BufferedWriter objfatal = new BufferedWriter (new FileWriter(ruta));
         objfatal.write("");
         objfatal.close();
       }
       catch(Exception objException){
           JOptionPane.showMessageDialog(null, "Error al reiniciar archivo");
               
       }
       }
}

package juego;
import javax.swing.JOptionPane;

public class Pregunta {
    
    private String pregunta;
    private Respuesta[] respuestasPosibles;
    public Pregunta(String pregunta, Respuesta[] respuestasPosibles) {
        this.pregunta = pregunta;
        this.respuestasPosibles = respuestasPosibles;
    }

    public void preguntar() {
        System.out.println(this.pregunta);
        char letraCorrecta = 'A';
        for (Respuesta opcion: this.respuestasPosibles) {
            if (opcion.esCorrecta()) letraCorrecta = opcion.getLetra();
            System.out.print(String.valueOf(opcion.getLetra()) + ")" + opcion.getRespuesta() + " ");
        }
        System.out.println("\nElige: ");
        Scanner sc = new Scanner(System.in);
        char letraElegidaPorElUsuario = sc.next().toUpperCase().charAt(0);
        if (letraElegidaPorElUsuario == letraCorrecta)
            System.out.println("Correcto");
        else
            System.out.println("Incorrecto, la respuesta correcta era " + String.valueOf(letraCorrecta));
    }
}

package juego;
import javax.swing.JOptionPane;

public class Respuesta {
   
    private String respuesta;
    private char Op;
    private boolean correcta;

    public Respuesta(String respuesta, char Op, boolean correcta) {
        this.respuesta = respuesta;
        this.Op = Op;
        this.correcta = correcta;
    }

    public String getRespuesta() {
        return this.respuesta;
    }

    public char getOp() {
        return this.Op;
    }

    public boolean Correcta() {
        return this.correcta;
    }

}
