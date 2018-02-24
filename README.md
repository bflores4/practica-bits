# practica-bits
private void btnprocesar_Click(object sender, EventArgs e)
		{
			Int32 entrada = Convert.ToInt32(txtentrada.Text);
			string sensorNivelDireccion = Convert.ToString(entrada, 2);
			lblBinario.Text = Convert.ToString(sensorNivelDireccion);
			txtsensor2.Text = Convert.ToString(Sensor2(entrada));
			txtsensor1.Text = Convert.ToString(Sensor1(entrada));
			Nivel(entrada);
			Direccion(entrada);
			txtFechaLectura.Text=Convert.ToString(FechaRead(entrada));
		}
	
		int Sensor1(Int32 numS1)
		{
			return (numS1 & 64) >> 6;
		}

		int Sensor2(Int32 numS2)
		{
			return (numS2 & 128) >> 7;
		}
   
		int Nivel(int numN)
		{
			int ambos = (byte)(numN >> 4);
			if (ambos == 2)
			{
				txtNivel.Text = "LLeno";
				return 2;
			}
			else if (ambos == 0)
			{
				txtNivel.Text = "Vacio";
				return ambos;
			}
			else if (ambos == 3)
			{
				txtNivel.Text = "LLenando";
				return ambos;
			}
			else
			{
				txtNivel.Text = "Nivel Medio";
				return 1;
			}
		}

		void Direccion(Int32 numD)
		{
			byte cardinal = (byte)(numD >> 1);
			cardinal = (byte)(numD & 7);
			switch (cardinal)
			{
				case 0:
					txtDireccion.Text = "N";//return 0
                    break;
				case 1:
					txtDireccion.Text = "NE";//return 1
                    break;
				case 2:
					txtDireccion.Text = "E";//return 2
                    break;
				case 3:
                    txtDireccion.Text = "SE";//return 3
					break;
				case 4:
					txtDireccion.Text = "S";//return 4
					break;
				case 5:
					txtDireccion.Text = "SO";//return 5
					break;
				case 6:
                    txtDireccion.Text = "O";//return 6
					break;
				case 7:
					txtDireccion.Text = "NO";//return 7
					break;
			}
						
		}

		void FechaDate(byte fechadia, byte fechames, byte fechayear)
		{
			byte Dia = fechadia;
			byte Mes = fechames;
			byte Year = fechayear;
			txtFechaLectura.Text = Dia.ToString() + "/" + Mes.ToString() + "/" + Year.ToString();
		}

		string FechaRead(Int32 date)
		{
			int Day = (date & 31);
			int Mnt = (date >> 5);
			int Month = (Mnt & 15);
			int Yr = (date >> 9);
			int Year = (Yr & 127);
			Year += 1900;
			string Fecha = Convert.ToString(Year) + "/" + Convert.ToString(Month) + "/" + Convert.ToString(Day);
			return Fecha;
		}

		void ChangeDate(int y, int m, int d)
		{
			Int32 Chg = 0;
			y -= 1900;
			Chg = (y << 9) + (m << 5) + (d);
			txtFechaCambiada.Text = Chg.ToString();
		}
		
		private void btndateChange_Click(object sender, EventArgs e)
		{
			DateTime dtf = dateTimeFecha.Value;
			string year = dtf.Year.ToString();
			string month = dtf.Month.ToString();
			string day = dtf.Day.ToString();
			int Y = Convert.ToInt32(year);
			int M = Convert.ToInt32(month);
			int D = Convert.ToInt32(day);
			ChangeDate(Y, M, D);
		}
