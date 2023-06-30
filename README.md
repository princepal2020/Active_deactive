# Active_deactive

public void Checkedgrid()
        {
            for (int i = 0; i < userGrid.Rows.Count; i++)
            {
                CheckBox check = (CheckBox)userGrid.Rows[i].Cells[0].FindControl("active_inactive");
                int id = Convert.ToInt32(((Label)userGrid.Rows[i].Cells[0].FindControl("txtid")).Text);
                if (check.Checked)
                {
                    string st = "FALSE";
                    SqlCommand cmd = new SqlCommand("update emp set active_inactuve='" + st + "' where id='" + id + "'", con);
                    cmd.CommandType = CommandType.Text;
                    con.Open();
                    cmd.ExecuteNonQuery();
                    con.Close();
                    userGrid.Rows[i].BackColor = Color.White;
                  
                }
                else
                {
                    string st = "TRUE";
                    SqlCommand cmd = new SqlCommand("update emp set active_inactuve='" + st + "' where id='" + id + "'", con);
                    cmd.CommandType = CommandType.Text;
                    con.Open();
                    cmd.ExecuteNonQuery();
                    con.Close();
                    userGrid.Rows[i].BackColor = Color.Wheat;
                   


                }
            }
        }

        protected void userGrid_RowDataBound(object sender, GridViewRowEventArgs e)
        {
            if (e.Row.RowType == DataControlRowType.DataRow)
            {
                Label mytotsale = (Label)e.Row.FindControl("lblstatus");
                //string status = mytotsale.Text.ToString();
                //if (!String.IsNullOrEmpty(status))
                //{
                if (mytotsale.Text.ToUpper() == "TRUE")
                {
                    CheckBox check = (CheckBox)e.Row.FindControl("active_inactive");
                    check.Checked = false;
                }
                else
                {
                    CheckBox check = (CheckBox)e.Row.FindControl("active_inactive");
                    check.Checked = true;
                }
                //}
            }


            
        }
