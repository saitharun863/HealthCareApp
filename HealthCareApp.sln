using System;
using System.Data;
using System.Data.Odbc;
using System.Data.SqlClient;
using System.Data.OleDb;

namespace HealthCareApp
{
    internal class Program
    {
        public static void AddPatient(SqlConnection conn)
        {
            Console.WriteLine("Enter Patient Name:");
            string Name = Console.ReadLine();
            Console.WriteLine("Enter Patient Age:");
            int Age = Convert.ToInt32(Console.ReadLine());
            Console.WriteLine("Enter Disease Description : ");
            string Disease = Console.ReadLine();

            string query = $"INSERT INTO Patient(Name,Age,Disease) VALUES('{Name}',{Age},'{Disease}');";
            
            SqlTransaction sqlTransaction = conn.BeginTransaction();
            try
            {
                using (SqlCommand cmd = new SqlCommand(query, conn, sqlTransaction))
                {
                    cmd.ExecuteNonQuery();
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine(ex.ToString());
            }
            sqlTransaction.Commit();
            Console.WriteLine("Transaction is Inserted and Committed!");
        }

        public static void UpdatePatient(SqlConnection conn)
        {
            Console.WriteLine("Enter Patient ID:");
            int P_id = Convert.ToInt32(Console.ReadLine());
            Console.WriteLine("Update Patient Name:");
            string Name = Console.ReadLine();
            Console.WriteLine("Update Patient Age:");
            int Age = Convert.ToInt32(Console.ReadLine());
            Console.WriteLine("Update Disease Description : ");
            string Disease = Console.ReadLine();

            string query = $"UPDATE Patient SET Name= '{Name}', Age = {Age}, Disease = '{Disease}' WHERE P_id = {P_id};";
            SqlTransaction sqlTransaction = conn.BeginTransaction();
            try
            {
                using (SqlCommand cmd = new SqlCommand(query, conn, sqlTransaction))
                {
                    cmd.ExecuteNonQuery();
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine(ex.ToString());
            }
            sqlTransaction.Commit();
            Console.WriteLine("Transaction is Updated and Committed!");
        }

        public static void DeletePatient(SqlConnection conn)
        {
            Console.WriteLine("Enter Patient ID to Delete :");
            int P_id = Convert.ToInt32(Console.ReadLine());

            string query = $"DELETE FROM Patient WHERE P_id = {P_id};";
            SqlTransaction sqlTransaction = conn.BeginTransaction();
            try
            {
                using (SqlCommand cmd = new SqlCommand(query, conn, sqlTransaction))
                {
                    cmd.ExecuteNonQuery();
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine(ex.ToString());
            }
            sqlTransaction.Commit();
            Console.WriteLine("Transaction is Deleted and Committed!");
        }

        public static void DisplayPatient(SqlConnection conn)
        {
            string query = "SELECT * FROM Patient";
            try
            {
                using (SqlDataAdapter adapter = new SqlDataAdapter(query, conn))
                {
                    DataSet ds = new DataSet();
                    adapter.Fill(ds, "Patient");
                    DataTable dt = ds.Tables["Patient"];
                    if (dt.Rows.Count <= 0)
                    {
                        Console.WriteLine("No Rows to Display");
                        return;
                    }
                    Console.WriteLine();
                    foreach (DataRow Row in dt.Rows)
                    {
                        Console.WriteLine($"Patient ID :{Row["P_id"]},\tName :{Row["Name"]},\tAge :{Row["Age"]},\tDisease: {Row["Disease"]}");
                    }
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine(ex.ToString());
            }
        }

        static void Main(string[] args)
        {
            string SqlConnStr = "Server=<your_Server_name>;Database=<your_database_name>;Trusted_Connection=True";
            using(SqlConnection conn = new SqlConnection(SqlConnStr))
            {
                conn.Open();
                Console.WriteLine("Connected to Database using SQL Client.");

                while (true)
                {
                    Console.WriteLine("\nCRUD Operations: \n1.Insert Patient Details\n2.Update Patient Details\n3.Delete Patient Details\n4.Display Details\n5.Exit");
                    Console.WriteLine("Enter Choice : ");
                    int ch = Convert.ToInt32(Console.ReadLine());
                    switch (ch) 
                    {
                        case 1: AddPatient(conn);break;
                        case 2: UpdatePatient(conn);break;
                        case 3: DeletePatient(conn);break;
                        case 4: DisplayPatient(conn);break;
                        case 5: return;
                        default: Console.WriteLine("Invalid Operation!!!");break;
                    }
                }
            }
        }
    }
}
