using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Windows.Forms;
using System.IO;

namespace RC4
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        

private void shifrFromTextBox_Click(object sender, EventArgs e)
        {

            RC4 s = new RC4();
            byte[] inpText;
            string Text = shifr_text.Text;
            inpText = new byte[Text.Length];
            for (int i = 0; i < Text.Length; i++)
            {
                inpText[i] = (byte)Text[i];
            }

            byte[] shuftText = s.Encode(inpText, inpText.Length);

            string st = "";
            for (int i = 0; i < inpText.Length; i++)
            {
                st += (char)shuftText[i];
            }
            zashifr_text.Text = st;

            SaveFileDialog saveFile = new SaveFileDialog();
            saveFile.DefaultExt = ".txt";
            saveFile.Filter = "text files ( *.txt)| *.txt";
            if(saveFile.ShowDialog() == DialogResult.OK && saveFile.FileName.Length > 0)
            {
                using (StreamWriter writer = new StreamWriter(saveFile.FileName, true))
                {
                    writer.WriteLine(zashifr_text.Text);
                    writer.Close();
                }
            }
        }

        private void shifrFromTXT_Click(object sender, EventArgs e)
        {
            OpenFileDialog openFile = new OpenFileDialog();
            openFile.Filter = "txt files( *.txt)|*.TXT";
            if(openFile.ShowDialog() == DialogResult.OK )
            {
                RC4 s = new RC4();
                byte[] inpText;
                StreamReader reader = new StreamReader(openFile.OpenFile());
                string Text = reader.ReadToEnd();
                shifr_text.Text = Text;
                inpText = new byte[Text.Length];
                for (int i = 0; i < Text.Length; i++)
                {
                    inpText[i] = (byte)Text[i];
                }

                byte[] shuftText = s.Encode(inpText, inpText.Length);

                string st = "";
                for (int i = 0; i < inpText.Length; i++)
                {
                    st += (char)shuftText[i];
                }
                zashifr_text.Text = st;
            }
        }

        private void deshifr_fromText_Click(object sender, EventArgs e)
        {
            RC4 s = new RC4();
            byte[] inpText;
            string Text = shifr_text2.Text;
            inpText = new byte[Text.Length];
            for (int i = 0; i < Text.Length; i++)
            {
                inpText[i] = (byte)Text[i];
            }

            byte[] shuftText = s.Decode(inpText, inpText.Length);

            string st = "";
            for (int i = 0; i < inpText.Length; i++)
            {
                st += (char)shuftText[i];
            }
            deshifr_text.Text = st;

            SaveFileDialog saveFile = new SaveFileDialog();
            saveFile.DefaultExt = ".txt";
            saveFile.Filter = "text files ( *.txt)| *.txt";
            if (saveFile.ShowDialog() == DialogResult.OK && saveFile.FileName.Length > 0)
            {
                using (StreamWriter writer = new StreamWriter(saveFile.FileName, true))
                {
                    writer.WriteLine(deshifr_text.Text);
                    writer.Close();
                }
            }

        }
