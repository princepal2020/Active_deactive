# Active_deactive
multi update
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

        Single update
           protected void active_inactive_CheckedChanged(object sender, EventArgs e)
        {
            string userid = Session["userid"].ToString();
            CheckBox chkBox = (CheckBox)sender;
            bool chec = Convert.ToBoolean(chkBox.Checked);
            GridViewRow row = (GridViewRow)chkBox.NamingContainer;
            int id = Convert.ToInt32(((Label)row.FindControl("lblID")).Text);
            string result = clsprpduct.ActiveDeActive(id, chec, userid);
            if (result == "Deactive")
            {
                Response.Write("<script>alert('Service Deactive successfully')</script>");

            }
            else if (result == "active")
            {
                Response.Write("<script>alert('Service Active successfully')</script>");

            }
            else
            {
                Response.Write("<script>alert('Error')</script>");
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
