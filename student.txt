import java.io.FileNotFoundException;
import java.io.IOException;
import java.io.PrintWriter;
import java.io.UnsupportedEncodingException;
import java.util.Scanner;
class Name
{
    String name;
    float regno;
    int n =0;
    float total_stud = 0f;
    Name(int x)
    {
        this.n = x;
    }

    Object[][] stud_vals = new Object[100][100];
    void enter_value()
    {
        for (int i = 0; i < n; i++)
        {
            for (int j = 0; j < 2; j++)
            {

                if (j == 0)
                {
                    int o = i+1;
                    System.out.println("Enter The Name of " + o + ".STUDENT :");
                    Scanner enter_item = new Scanner(System.in);
                    name = enter_item.nextLine();
                    stud_vals[i][0] = name;
                } else
                {
                    int p = i+1;
                    System.out.println("Enter The  Reg. no. of " + p + ".STUDENT :");
                    Scanner enter_price = new Scanner(System.in);
                    regno = enter_price.nextFloat();
                    stud_vals[i][1] = regno;
                    this.total_stud = n;
                }
            }
        }
    }
    void show_values()
    {
        System.out.println("STUDENT NAME   REG. NUMBER");
        for (int i=0;i<this.n;i++)
        {
            System.out.println(stud_vals[i][0]+"   "+stud_vals[i][1]);
        }
        System.out.println("       TOTAL STUDENTS");
        System.out.println("       "+this.total_stud);
    }
}
class sections extends Name
{
    float section_n = 0f;
    float ans = 0f;

    sections(int x) {
        super(x);
    }
    void enter_value(float y)
    {
        this.section_n = y;
        this.ans = super.total_stud/this.section_n;
        System.out.println("No. of Sections to be created : "+this.section_n);
        System.out.println("Total Approx. Student per Section : "+this.ans);
    }
    class genFile
    {
        String filename;
        genFile(String d)
        {
            this.filename = d;
        }
        void mk_file() throws FileNotFoundException
        {

            PrintWriter writer = new PrintWriter(this.filename+".txt");
            writer.println("STUDENT NAME   REG. NUMBER");
            for (int i=0;i<sections.super.n;i++)
            {
                writer.println(stud_vals[i][0]+"   "+stud_vals[i][1]);
            }
            writer.println("Sections  : "+section_n);
            writer.println("Total Approx. Student per Section : "+ans);
            writer.flush();
            writer.close();
        }
    }
}
class SM_system
{
    public static void main(String[] args) throws FileNotFoundException
    {
        int no = 1;
        float sal = 3000;
        String date;
        System.out.println("Enter the Number of students : ");
        Scanner no_enter = new Scanner(System.in);
        no = no_enter.nextInt();
        sections i1 = new sections(no);
        i1.enter_value();
        i1.show_values();
        System.out.println("Enter the Total Number of sections");
        Scanner sal_enter = new Scanner(System.in);
        sal = sal_enter.nextFloat();
        i1.enter_value(sal);
        System.out.println("Enter today's To Generate a File");
        Scanner file_name_date = new Scanner(System.in);
        date = file_name_date.nextLine();
        sections.genFile g1 = i1.new genFile(date);
        g1.mk_file();
    }
}
