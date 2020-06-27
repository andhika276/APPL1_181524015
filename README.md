# APPL1_181524015
Pengerjaan SOLID, Memperbaiki Kode

1. Stream Progress

Prinsip design yang digunakan pada kode ini yaitu OPC yaitu (Open Closed Principle)
 Principle ini digunakan agar memudahkan programer lain mengextend atau menambahkan kode hanya dengan menambah class baru tanpa mengubah class lainnya
 
 public interface IStreamable
{
    int Length { get; }

    int BytesSent { get; }
}
namespace _01.Stream_Progress
{
    public class StreamProgressInfo
    {
        private IStreamable file;
    
        public StreamProgressInfo(IStreamable file)
        {
            this.file = file;
        }

        public int CalculateCurrentPercent()
        {
            return file.BytesSent * 100 / file.Length;
        }
    }
}

 namespace _01.Stream_Progress
{
    public class File : IStreamable
    {
        private string name;

        public File(string name, int length, int bytesSent)
        {
            this.name = name;
            Length = length;
            BytesSent = bytesSent;
        }

        public int Length { get; set; }

        public int BytesSent { get; set; }
    }
}


Untuk menambahkan stream baru maka bisa membuat kelas dengan spesifikasi seperti file atau music
sehingga tidakmerusak class iStream dan interface.

2. Graphics Editor
Prinsip design yang digunakan pada kode ini yaitu Interface Segregation Principle 
patern ini digunakan agar tidakmengaskes ke objeknya langsung sehingga digunakanlah prinsip ini

 
 namespace _02.Graphic_Editor
{
    using System;

    public class GraphicEditor
    {
        public void DrawShape(IShape shape)
        {
            Console.WriteLine(shape.Drow());
        }
    }
}

namespace _02.Graphic_Editor
{
    public interface IShape
    {
        string Drow();
    }
}

namespace _02.Graphic_Editor
{
    public class Rectangle : IShape
    {
       public string Drow()
        {
           return "I'm Rectangle";
        }
    }
}
﻿namespace _02.Graphic_Editor
{
    public class Startup
    {
        public static void Main()
        {
            var circle = new Circle();
            var rect = new Rectangle();
            var square = new Square();

            var editor=new GraphicEditor();
            editor.DrawShape(circle);
            editor.DrawShape(rect);
            editor.DrawShape(square);
        }
    }
}

Dengan kode seperti diatas Dengan interface maka mudah untuk mengakses tanpa mengunakan objek circle secata langsung

3. Detail Printer
Prinsip design yang digunakan pada kode ini yaitu DIP singkatan dari Dependency Inversion
Pengertian dari prinsip ini adalah bahwa class yang dikategorikan sebagai high-level class 
 tidak boleh bergantung pada low-level class tetapi harus bergantung pada abstraksi. 
 Sehingga tidak terjadinya tight coupling
 
 ﻿namespace _03.Detail_Printer
{
    public class Employee
    {
        public Employee(string name)
        {
            this.Name = name;
        }

        public string Name { get; private set; }

        public override string ToString()
        {
            return this.Name;
        }
    }
}
﻿using System;

namespace _03.Detail_Printer
{
    using System.Collections.Generic;

    public class Manager : Employee
    {
        public Manager(string name, ICollection<string> documents) 
            : base(name)
        {
            this.Documents = new List<string>(documents);
        }

        public IReadOnlyCollection<string> Documents { get; set; }

        public override string ToString()
        {
            return base.ToString() + Environment.NewLine + string.Join(Environment.NewLine, this.Documents);
        }
    }
}

Dengan kode seperti diatas Dengan begini class Startup tidak terikat secara langsung dengan setiap
class mengurus isi dari method masing masing, high-level class seperti Startup tidak perlu khawatir dengan perubahan tersebut.


