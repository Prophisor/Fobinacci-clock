using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace Fobinacci_Uhr
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
            // Add manual controls initialization
            InitializeManualControls();
        }

        private void InitializeManualControls()
        {
            // Button: Set Time
            var btnSetTime = new Button();
            btnSetTime.Text = "Set Time";
            btnSetTime.Location = new System.Drawing.Point(350, 360);
            btnSetTime.Size = new System.Drawing.Size(75, 26);
            btnSetTime.Click += BtnSetTime_Click;
            this.Controls.Add(btnSetTime);

            // Button: Start Auto
            var btnStartAuto = new Button();
            btnStartAuto.Text = "Start";
            btnStartAuto.Location = new System.Drawing.Point(430, 360);
            btnStartAuto.Size = new System.Drawing.Size(40, 26);
            btnStartAuto.Click += BtnStartAuto_Click;
            this.Controls.Add(btnStartAuto);

            // Button: Stop Auto
            var btnStopAuto = new Button();
            btnStopAuto.Text = "Stop";
            btnStopAuto.Location = new System.Drawing.Point(475, 360);
            btnStopAuto.Size = new System.Drawing.Size(40, 26);
            btnStopAuto.Click += BtnStopAuto_Click;
            this.Controls.Add(btnStopAuto);
        }

        private void BtnSetTime_Click(object sender, EventArgs e)
        {
            int h = (int)this.Stunden.Value;
            int m = (int)this.Minuten.Value;
            this.lblLiveTime.Text = string.Format("{0:00}:{1:00}:00", h, m);
            if (this.timer1 != null)
            {
                this.timer1.Enabled = false;
            }
        }

        private void BtnStartAuto_Click(object sender, EventArgs e)
        {
            if (this.timer1 == null)
            {
                // Ensure a container exists so Dispose works as expected
                if (this.components == null)
                {
                    this.components = new System.ComponentModel.Container();
                }
                this.timer1 = new System.Windows.Forms.Timer(this.components);
                this.timer1.Interval = 1000;
                this.timer1.Tick += new EventHandler(this.timer1_Tick);
            }
            this.timer1.Enabled = true;
        }

        private void BtnStopAuto_Click(object sender, EventArgs e)
        {
            if (this.timer1 != null)
            {
                this.timer1.Enabled = false;
            }
        }

        // Werte der existierenden Blöcke (ohne den speziellen 12er-Block)
        private readonly int[] blockWerte = new[] { 5, 3, 2, 1 };
        private List<int> stundenWerte = new List<int>();

        private void numericUpDown1_ValueChanged(object sender, EventArgs e)
        {
            Hintergrund_St();
            stundenWerte.Clear();

            int stunden = Decimal.ToInt32(Stunden.Value);
            int minuten = Decimal.ToInt32(Minuten.Value);

            Stunden_rechnen(stunden);

            int minutenTeile = minuten / 5; // Minuten werden in 5-Minuten-Schritten dargestellt
            foreach (var wert in blockWerte)
            {
                if (minutenTeile >= wert)
                {
                    minutenTeile -= wert;
                    var ctrl = GetControlFürWert(wert);
                    if (ctrl != null)
                    {
                        ctrl.BackColor = stundenWerte.Contains(wert) ? Color.Blue : Color.Green;
                    }
                }
            }
        }

        private void Stunden_rechnen(int stundenzahl)
        {
            if (stundenzahl == 12)
            {
                // Spezialfall: 12 wird mit dem eigenen Block angezeigt
                St12.BackColor = Color.Red;
                stundenWerte.Add(12);
                return;
            }

            foreach (var wert in blockWerte)
            {
                if (stundenzahl >= wert)
                {
                    stundenzahl -= wert;
                    stundenWerte.Add(wert);
                    SetBlockFarbe(wert, Color.Red);
                }
            }
        }

        private Control GetControlFürWert(int wert)
        {
            switch (wert)
            {
                case 5: return St5;
                case 3: return St3;
                case 2: return St2;
                case 1: return St1;
                default: return null;
            }
        }

        private void SetBlockFarbe(int wert, Color farbe)
        {
            switch (wert)
            {
                case 1: St1.BackColor = farbe; break;
                case 2: St2.BackColor = farbe; break;
                case 3: St3.BackColor = farbe; break;
                case 5: St5.BackColor = farbe; break;
                case 12: St12.BackColor = farbe; break;
            }
        }

        private void Hintergrund_St()
        {
            St1.BackColor = Color.White;
            St2.BackColor = Color.White;
            St3.BackColor = Color.White;
            St5.BackColor = Color.White;
            St12.BackColor = Color.White;
        }

        private void timer1_Tick(object sender, EventArgs e)
        {
            // Aktuelle Uhrzeit holen
            var now = DateTime.Now;
            // Stunden im 12-Stunden-Format
            int currentHour = now.Hour % 12;
            if (currentHour == 0) currentHour = 12;
            int currentMinute = now.Minute;

            // Minuten auf nächstes 5-Minuten-Schritt abrunden
            int minuteRounded = (currentMinute / 5) * 5;

            // Werte in die NumericUpDowns eintragen ohne ValueChanged-Events zu triggern
            // Temporär Event-Handler entfernen
            Stunden.ValueChanged -= numericUpDown1_ValueChanged;
            Minuten.ValueChanged -= numericUpDown1_ValueChanged;
            try
            {
                Stunden.Value = currentHour;
                Minuten.Value = minuteRounded;
            }
            finally
            {
                // Handler wieder hinzufügen
                Stunden.ValueChanged += numericUpDown1_ValueChanged;
                Minuten.ValueChanged += numericUpDown1_ValueChanged;
            }

            // Manuell Anzeige aktualisieren
            numericUpDown1_ValueChanged(this, EventArgs.Empty);
            // Live-Zeitanzeige aktualisieren
            if (this.lblLiveTime != null)
            {
                this.lblLiveTime.Text = now.ToString("HH:mm:ss");
            }
        }


    }

       

        
}
