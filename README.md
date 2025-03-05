Proxy
public interface IDocumento
{
    void Mostrar();
}
using System;

public class Documento : IDocumento
{
    private string _nombreArchivo;

    public Documento(string nombreArchivo)
    {
        _nombreArchivo = nombreArchivo;
        CargarDesdeDisco();
    }

    private void CargarDesdeDisco()
    {
        Console.WriteLine($"Cargando documento desde el disco: {_nombreArchivo}");
    }

    public void Mostrar()
    {
        Console.WriteLine($"Mostrando documento: {_nombreArchivo}");
    }
}
using System;

public class ProxyDocumento : IDocumento
{
    private Documento _documentoReal;
    private string _nombreArchivo;

    public ProxyDocumento(string nombreArchivo)
    {
        _nombreArchivo = nombreArchivo;
    }

    public void Mostrar()
    {
        if (_documentoReal == null)
        {
            _documentoReal = new Documento(_nombreArchivo);
        }
        _documentoReal.Mostrar();
    }
}
class Program
{
    static void Main()
    {
        IDocumento documento = new ProxyDocumento("archivo.pdf");

        // El documento no se carga hasta que se llame a Mostrar()
        Console.WriteLine("El documento aún no se ha cargado...");

        // Ahora se carga y se muestra
        documento.Mostrar();

        // La segunda vez, ya no se vuelve a cargar, solo se muestra
        documento.Mostrar();
    }
}
El documento aún no se ha cargado...
Cargando documento desde el disco: archivo.pdf
Mostrando documento: archivo.pdf
Mostrando documento: archivo.pdf

