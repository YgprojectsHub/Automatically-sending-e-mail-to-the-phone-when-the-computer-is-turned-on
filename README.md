# Automatically-sending-e-mail-to-the-phone-when-the-computer-is-turned-on

#Microsoft Visiul Studıo 2019

using System;

using System.Collections.Generic;

using System.ComponentModel;

using System.Data;

using System.Drawing;

using System.Linq;

using System.Text;

using System.Threading.Tasks;

using System.Windows.Forms;

using Microsoft.Win32;

using System.Net;

using System.Net.Mail;

namespace sesdöviz
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        private void Form1_Load(object sender, EventArgs e)
        {
            RegistryKey key = Registry.CurrentUser.OpenSubKey(@"Software\Microsoft\Windows\CurrentVersion\Run", true);
            key.SetValue("sesdöviz", "\"" + Application.ExecutablePath + "\"");

            this.Left = System.Windows.Forms.Screen.PrimaryScreen.WorkingArea.Right - this.Width;
            this.Top = System.Windows.Forms.Screen.PrimaryScreen.WorkingArea.Height - this.Height;

            Gonder();
        }

        private void button1_Click(object sender, EventArgs e)
        {
            Application.Exit();
        }

        MailMessage ePosta = new MailMessage();

        void Gonder()
        {
            string contents = "//Contents";
            string theme = "//Theme";

            ePosta.From = new MailAddress("youraccount@outlook.com");
            
            ePosta.To.Add("addresstosend@outlook.com");

            ePosta.Subject = theme;
            
            ePosta.Body = contents;
            
            SmtpClient smtp = new SmtpClient();
            
            smtp.Credentials = new System.Net.NetworkCredential("youraccount@outlook.com", "yourpassword");
            smtp.Host = "smtp.live.com"; 
            smtp.EnableSsl = true;
            smtp.Port = 587;

            smtp.Send(ePosta);
        }
    }
}
