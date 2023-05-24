# Deal_to_project_HTML-page

the inly html page will be display on widget
###################Custom Button##################

get_var = zoho.crm.getOrgVariable("dealtoprojectmappingforzohocrm__Field_Mapping");
info get_var;
cust_stage = get_var.getJSON("pick_list_values");
// info cust_stage;
// dealid = "4619457000019908001";
dealid = deal.getJSON("Deals.ID").getJSON("Deals.ID");
//info dealid;
deal_data = zoho.crm.getRecordById("deals",dealid);
// deal_data = zoho.crm.getRecordById("deals","4555187000025033035");
// info "deal_data   "+deal_data;
stage = deal_data.getJSON("Stage");
// info stage;
Portal = get_var.getJSON("Portal").getJSON("value");
info "portal " + Portal;
// Portal = "718748180";
// Contact = Deal_records.getJSON("Contact_Name");
Contact = deal_data.getJSON("Contact_Name");
info "contact " + Contact;
// //info stage;
if(stage == cust_stage)
{
	// 	dynamic_map = Map();
	Owner = deal_data.getJSON("Owner");
	// 	info Owner;
	id = Owner.getJSON("id");
	name = Owner.getJSON("name");
	Email = Owner.get("email");
	Deal_filds = get_var.getJSON("D_Array");
	// 	info Deal_filds;
	cust_deal_name = Deal_filds.getJSON("Deal_name2");
	name = deal_data.getJSON(cust_deal_name);
	info name;
	// 	**start date
	cust_startdate = Deal_filds.getJSON("ST_date");
	if(cust_startdate != null)
	{
		if(cust_startdate != "undefined")
		{
			if(cust_startdate != "None")
			{
				start_date = deal_data.getJSON(cust_startdate);
				// 			info start_date;
				if(start_date != null)
				{
					st_date = start_date.toString("MM-dd-yyyy");
					Sdate = st_date;
					// 				info Sdate;
				}
				else
				{
					st_date = zoho.currentdate.toString("MM-dd-yyyy");
					Sdate = st_date;
					// 				info Sdate;
				}
			}
			else
			{
				st_date = zoho.currentdate.toString("MM-dd-yyyy");
				Sdate = st_date;
				// 			info Sdate;
			}
		}
		else
		{
			st_date = zoho.currentdate.toString("MM-dd-yyyy");
			Sdate = st_date;
			// 		info Sdate;
		}
	}
	else
	{
		st_date = zoho.currentdate.toString("MM-dd-yyyy");
		Sdate = st_date;
	}
	// 	**end date
	cust_enddate = Deal_filds.getJSON("ED_date");
	if(cust_enddate != null)
	{
		if(cust_enddate != "undefined")
		{
			if(cust_enddate != "None")
			{
				end_date = deal_data.getJSON(cust_enddate);
				// 			info end_date;
				if(end_date != null)
				{
					en_date = end_date.toString("MM-dd-yyyy");
					edate = en_date;
					// 				info edate;
				}
				else
				{
					en_date = zoho.currentdate.toString("MM-dd-yyyy");
					edate = en_date.addDay(1).toString("MM-dd-yyyy");
					// 				info edate;
				}
			}
			else
			{
				en_date = zoho.currentdate.toString("MM-dd-yyyy");
				edate = en_date.addDay(1).toString("MM-dd-yyyy");
				//info edate;
			}
		}
		else
		{
			en_date = zoho.currentdate.toString("MM-dd-yyyy");
			edate = en_date.addDay(1).toString("MM-dd-yyyy");
			//info edate;
		}
	}
	else
	{
		en_date = zoho.currentdate.toString("MM-dd-yyyy");
		edate = en_date.addDay(1).toString("MM-dd-yyyy");
	}
	//** compare start date and end date
	// 	if(start_date != null && end_date != null)
	// 	{
	if(edate.toDate() >= Sdate.toDate())
	{
	}
	else
	{
		info 'date not vlaid';
		return "Please select the proper date fields End Date must grater then Start Date";
	}
	//}
	// 		**description
	cust_Disc = Deal_filds.getJSON("Disc");
	if(cust_Disc != null)
	{
		descri = deal_data.getJSON(cust_Disc);
		if(cust_Disc != "undefined")
		{
			descri = deal_data.getJSON(cust_Disc);
			if(cust_Disc != "None")
			{
				descri = ifnull(deal_data.getJSON(cust_Disc)," ");
				info "descri" + descri;
			}
		}
	}
	// 		** currency INR
	Currency_deal = deal_data.getJSON("Currency");
	info "Currency_deal" + Currency_deal;
	// 		**budget type
	budget2 = Deal_filds.getJSON("budget2");
	info "budget2" + budget2;
	if(budget2 != null)
	{
		if(budget2 != "undefined")
		{
			if(budget2 != "None")
			{
				budgettype = budget2;
			}
			else
			{
				budgettype = 0;
			}
		}
		else
		{
			budgettype = 0;
		}
	}
	else
	{
		budgettype = 0;
	}
	// 		**project value
	pro_bud = Deal_filds.getJSON("pro_bud");
	info "Budget_type  " + pro_bud;
	Project_amount = deal_data.getJSON(pro_bud);
	info "pr amount " + Project_amount;
	if(budget2 != null)
	{
		if(pro_bud != null)
		{
			if(pro_bud != "undefined")
			{
				if(budget2 != "None")
				{
					if(pro_bud == "No data available")
					{
						// 			Project_amount = deal_data.getJSON(pro_bud);
						info "project_amount " + Project_amount;
						//	dynamic_map.put("budget_value",0);
						probudjet = 0;
						// 			if (probudjet == null)
						//             {
						// // 				dynamic_map.put("budget_value",0);
						//             }
						// 			else 
						//             {
						// 				dynamic_map.put("budget_value",0);
						//             }
					}
					if(pro_bud != "None")
					{
						probudjet = deal_data.getJSON(pro_bud);
					}
					else
					{
						probudjet = deal_data.getJSON("Amount");
					}
				}
				else
				{
					probudjet = 0;
				}
			}
			else
			{
				probudjet = deal_data.getJSON("Amount");
			}
		}
		else
		{
			probudjet = deal_data.getJSON("Amount");
		}
	}
	else
	{
		probudjet = 0;
	}
	//** billing method
	billing = Deal_filds.get("billing");
	// 	info billing;
	if(billing != null)
	{
		if(billing != "undefined")
		{
			if(billing != "None")
			{
				if(billing == 3)
				{
					fixedcost = deal_data.getJSON("Amount");
				}
				else
				{
					fixedcost = 0;
				}
			}
			else
			{
				billing = 1;
				fixedcost = 0;
			}
		}
		else
		{
			fixedcost = 0;
			billing = 1;
		}
	}
	else
	{
		fixedcost = 0;
		billing = 1;
	}
	//** get portal
	//** mapping create project
	// 	dynamic_map = Map();
	// 	//Map all dynamic params to your desired values 
	// 	dynamic_map.put("protalid",Portal);
	// 	dynamic_map.put("name",name);
	// 	dynamic_map.put("start_date",Sdate);
	// 	dynamic_map.put("end_date",edate);
	// 	dynamic_map.put("description",descri);
	// 	dynamic_map.put("currency","INR");
	// 	dynamic_map.put("budget_type",budgettype);
	// 	dynamic_map.put("budget_value",probudjet);
	// 	dynamic_map.put("fixed_cost",fixedcost);
	// 	dynamic_map.put("billing_method",billing);
	// 	info dynamic_map;
	projectName = zoho.encryption.urlEncode(name);
	// 	info projectName;
	projectDescription = zoho.encryption.urlEncode(descri);
	dynamic_map = Map();
	//Map all dynamic params to your desired values 
	dynamic_map.put("protalid",Portal);
	dynamic_map.put("name",projectName);
	dynamic_map.put("start_date",Sdate);
	dynamic_map.put("end_date",edate);
	dynamic_map.put("description",projectDescription);
	dynamic_map.put("currency",Currency_deal);
	dynamic_map.put("budget_type",budgettype);
	dynamic_map.put("budget_value",probudjet);
	dynamic_map.put("fixed_cost",fixedcost);
	dynamic_map.put("billing_method",billing);
	//zoho.crm.invokeconnector("dealtoprojectmappingforzohocrm.zohoprojectconnector.createproject",dynamic_map);
	create_project = zoho.crm.invokeConnector("dealtoprojectmappingforzohocrm.zohoprojectconnector.createproject",dynamic_map);
	info create_project;
	status_code = create_project.getJSON("status_code");
	if(status_code == 201)
	{
		//Project_name = Deal_records.getJSON(dcust1);
		if(Contact.size() > 0)
		{
			Contact_Id = Contact.getJSON("id");
			// 			info "Contact_Name: " + Contact_Id;
			Contact = zoho.crm.getRecordById("contacts",Contact_Id);
			Contact_email = Contact.getJson("Email");
			namespace = "dealtoprojectmappingforzohocrm__signal";
			subject = "Deal" + name + "created Project";
			message = "A new project " + name + " has been created from the deal " + name;
			signalMap = Map();
			signalMap.put("signal_namespace",namespace);
			signalMap.put("email",Contact_email);
			signalMap.put("subject",subject);
			signalMap.put("message",message);
			result = zoho.crm.raiseSignal(signalMap);
		}
		sendmail
		[
			from :zoho.adminuserid
			to :Email
			subject :"Deal " + name + " converted project "
			message :"A new project " + name + " has been created from the deal  " + name
		]
		return name + " created successfully in Zoho Projects";
	}
	else
	{
		if(status_code == 400)
		{
			return "Please try to create a deal again because there was an error with filling out the fields.";
		}
		else
		{
			response = create_project.getJSON("response");
			//info response;
			error = response.getJSON("error");
			if(error != null)
			{
				details = error.getJSON("details");
				//info details;
				field_name = details.getJSON("field_name");
				info field_name;
				if(field_name == "currency")
				{
					return "The currency field must be the same in Zoho CRM and Zoho Projects.";
				}
			}
		}
	}
}
else
{
	return "Please select the appropriate stage.You have selected stage is " + cust_stage + " in Setting page";
}
return "";
