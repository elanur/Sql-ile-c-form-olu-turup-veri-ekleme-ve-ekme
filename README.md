# Sql ile basit veri-ekleme-ve cekme
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;
using System.Data.SqlClient;

namespace Kayıt
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        private void label2_Click(object sender, EventArgs e)
        {

        }

        private void label4_Click(object sender, EventArgs e)
        {

        }

        private void button1_Click(object sender, EventArgs e)
        {
            SqlConnection baglanti = new SqlConnection("Data Source=SAMSUNG;Initial Catalog=Deneme;Integrated Security=True");
            baglanti.Open();
            SqlCommand cmd = new SqlCommand("Select * from Kayıt where Kullanıcı_Adı ='" + textBox1.Text + "'and Şifre='" + textBox2.Text + "'", baglanti);
            SqlDataReader rd;
            rd = cmd.ExecuteReader();
            int count = 0;
            while(rd.Read())
            {
                count +=1;
            }
        if(count==1)
        {
            MessageBox.Show("Giriş Yapıldı");
            Form2 f2=new Form2();
            f2.Show();
           
            
        }
        else if (count>0)
        {
            MessageBox.Show("Bir Hata Meydana geldi :(");
        }
        else
        {
            MessageBox.Show("Kullanıcı adı veya Şifre Yanlış");
        }
            textBox1.Clear();
            textBox2.Clear();
        }

        private void button2_Click(object sender, EventArgs e)
        {
            SqlConnection baglanti = new SqlConnection("Data Source=SAMSUNG;Initial Catalog=Deneme;Integrated Security=True");
            baglanti.Open();
           
            SqlDataAdapter cd = new SqlDataAdapter("insert into Kayıt (Adı,Soyadı,[E-posta],Kullanıcı_Adı,Şifre) values ('" + textBox3.Text + "','" + textBox4.Text + "','" + textBox5.Text + "','" + textBox6.Text + "','" + textBox7.Text + "')", baglanti);
            cd.SelectCommand.ExecuteNonQuery();
            baglanti.Close();
            MessageBox.Show("Müşteri Kayıt İşlemi Gerçekleşti.");
            Form2 f1 = new Form2();
            f1.Show();
            textBox3.Clear();
            textBox4.Clear();
            textBox5.Clear();
            textBox6.Clear();
            textBox7.Clear();
               

        }
    }
}
