using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;
using System.Threading;

namespace StockExchange
{
    public partial class Login : Form
    {
        Thread thread;
        private String UserType;
        private String UserId;
        private String PassWord;
        Controller controller = new Controller();
        public Login()
        {
            InitializeComponent();
        }

        private void button1_Click(object sender, EventArgs e)
        {
            UserId = textBox1.Text;
            PassWord = textBox2.Text;
            UserType = controller.LoginCheck(UserId, PassWord);

            if (UserType == null)
            {
                UserType = "Login failed";
                textBox3.Text = UserType;

            }
            else
            {

                this.Close();
                thread = new Thread(OpenNewForm);
                thread.SetApartmentState(ApartmentState.STA);
                thread.Start();
            }


        }
        private void OpenNewForm()
        {
            Application.Run(new Form2(UserId, UserType));
        }

        private void textBox1_TextChanged(object sender, EventArgs e)
        {

        }

        private void textBox3_TextChanged(object sender, EventArgs e)
        {

        }

        private void textBox2_TextChanged(object sender, EventArgs e)
        {

        }
    }
}
