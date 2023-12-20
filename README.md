<Window x:Class="jakiescos.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:local="clr-namespace:jakiescos"
        mc:Ignorable="d"
        Title="MainWindow" Height="450" Width="800">
    <Grid>
        <Grid.ColumnDefinitions>
            <ColumnDefinition Width="*"></ColumnDefinition>
            <ColumnDefinition Width="*"></ColumnDefinition>
        </Grid.ColumnDefinitions>
        <Grid.RowDefinitions>
            <RowDefinition></RowDefinition>
            <RowDefinition></RowDefinition>
            <RowDefinition></RowDefinition>
            <RowDefinition></RowDefinition>
            <RowDefinition></RowDefinition>
        </Grid.RowDefinitions>

        <Grid Grid.ColumnSpan="2" Grid.Row="0" Visibility="Visible" x:Name="grid1">
            <Grid.ColumnDefinitions>
                <ColumnDefinition Width="*"></ColumnDefinition>

            </Grid.ColumnDefinitions>
            <Grid.RowDefinitions>
                <RowDefinition></RowDefinition>
                <RowDefinition></RowDefinition>
            </Grid.RowDefinitions>
            <TextBlock Grid.Row="0" Grid.Column="0">Podaj poczatek</TextBlock>
            <Slider Grid.Row="1" Grid.Column="1" Minimum="0" Maximum="100" x:Name="s1"></Slider>
        </Grid>

        <Grid Grid.ColumnSpan="2" Grid.Row="1" Visibility="Visible" x:Name="grid2">
            <Grid.ColumnDefinitions>
                <ColumnDefinition Width="*"></ColumnDefinition>

            </Grid.ColumnDefinitions>
            <Grid.RowDefinitions>
                <RowDefinition></RowDefinition>
                <RowDefinition></RowDefinition>
            </Grid.RowDefinitions>
            <TextBlock Grid.Row="0" Grid.Column="0">Podaj koniec</TextBlock>
            <Slider Grid.Row="1" Grid.Column="1" Minimum="100" Maximum="1000" x:Name="s2"></Slider>
        </Grid>

        <Button Grid.ColumnSpan="2" Grid.Row="2" Width="100" Height="50" Click="Losuj" Visibility="Visible" x:Name="g1">Losuj liczbe</Button>

        <TextBlock Grid.Column="0" Grid.Row="3" TextAlignment="Center" FontSize="30" Visibility="Hidden" x:Name="tekst">Podaj liczbe</TextBlock>
        <TextBox Grid.Column="1" Grid.Row="3" Height="60" Width="300" Visibility="Hidden" x:Name="tu"></TextBox>


        <TextBlock Grid.Column="0" Grid.Row="4" Visibility="Hidden" x:Name="tekst2">Z zakresu</TextBlock>
        <Button Grid.Column="1" Grid.Row="4" Width="100" Height="50" Visibility="Hidden" x:Name="g2" Click=">Dalej</Button>
    </Grid>
</Window>






using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Data;
using System.Windows.Documents;
using System.Windows.Input;
using System.Windows.Media;
using System.Windows.Media.Imaging;
using System.Windows.Navigation;
using System.Windows.Shapes;

namespace jakiescos
{
    /// <summary>
    /// Interaction logic for MainWindow.xaml
    /// </summary>
    public partial class MainWindow : Window
    {
        public MainWindow()
        {
            InitializeComponent();
        }

        int x = 0;
        int strzal;
        int ile = 0;
        private void Losuj(object sender, RoutedEventArgs e)
        {
            int a = (int)s1.Value;
            int b = (int)s2.Value;
            Random random = new Random();

            x = random.Next(a, b);

            tekst2.Text = "Z zakresu "+a+" - "+b;
            
            tekst.Visibility= Visibility.Visible;
            tekst2.Visibility = Visibility.Visible;
            g1.Visibility = Visibility.Collapsed;
            g2.Visibility = Visibility.Visible;
            grid1.Visibility = Visibility.Collapsed;
            grid2.Visibility = Visibility.Collapsed;
            tu.Visibility = Visibility.Visible;
        }

        private void Dalej(object sender, RoutedEventArgs e)
        {
            if (int.TryParse(tu.Text, out strzal))
            {
                if(strzal == x)
                {
                    MessageBox.Show("Gratulacje trafiles za"+ile+"razem");
                }
                if (strzal < x)
                {
                    MessageBox.Show("Za malo");
                    ile++;
                }
                if (strzal> x)
                {
                    MessageBox.Show("Za duzo");
                    ile++;
                }

            }
        }
    }
}
