# MP4-to-MP3-convertor
//For education pourpos only

using System;
using System.Windows.Forms;

namespace Convertor
{
    public partial class Converter : Form
    {
        String Videopath, Videoname, Savepath, Savename;

        private void VideoIn_Click(object sender, EventArgs e)
        {
            OpenFileDialog openFileDialog = new OpenFileDialog()
            {
                Multiselect = false,
                Filter = "MP4 File|*.mp4"
            };
            if (openFileDialog.ShowDialog() == DialogResult.OK)
            {
                Videopath = openFileDialog.FileName;
                Videoname = openFileDialog.SafeFileName;

            }
            TextBox1.Text = Videopath;
        }

        private void VideoSave_Click(object sender, EventArgs e)
        {
            FolderBrowserDialog folderBrowserDialog = new FolderBrowserDialog();
            if (folderBrowserDialog.ShowDialog() == DialogResult.OK)
            {
                Savepath = folderBrowserDialog.SelectedPath;
                Savename = Videoname.Substring(0, Videoname.Length - 4);
                Savepath += ("\\" + Savename + ".mp3");
            }
            Textbox2.Text = Savepath;
        }

        private void VideoCon_Click(object sender, EventArgs e)
        {
            var convert = new NReco.VideoConverter.FFMpegConverter();
            convert.ConvertMedia(TextBox1.Text.Trim(), Textbox2.Text.Trim(), "mp3");
        }

        public Converter()
        {
            InitializeComponent();
        }

        private void label1_Click(object sender, EventArgs e)
        {

        }

        private void Form1_Load(object sender, EventArgs e)
        {

        }
    }
}
