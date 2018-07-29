# -*- coding: utf-8 -*-
# -------------------------------------------------------------------------
# This is a sample controller
# this file is released under public domain and you can use without limitations
# -------------------------------------------------------------------------

# ---- example index page ----
def index():
    
    response.flash = T("Hi")
    return dict(message=T('Welcome to web2py!'))

# ---- API (example) -----
@auth.requires_login()
def api_get_user_email():
    if not request.env.request_method == 'GET': raise HTTP(403)
    return response.json({'status':'success', 'email':auth.user.email})
def doctor():
    
    #db.Patient.prescription.show_if=(db.patientAccess.access==True)
    response.flash = T("Hi")
    return dict(message=T('Welcome to web2py!'))
   # prob=db(db.Patient).select()
def doctor_unpermitpatient():
    query=((db.Doctoraccess.Patient_Permit==False)and(db.Doctoraccess.Doctor_Request==False))
    fields = (db.Doctoraccess.Doctor_name,db.Doctoraccess.specialisation, db.Doctoraccess.Patient_name,  db.Doctoraccess.Doctor_Request)
    
    sol = SQLFORM.grid(query=query,fields=fields,user_signature = False,deletable=False,details=False)
    return dict(sol=sol)
    
def doctor_permitpatient():
    sol=SQLFORM.grid(db.Patient,user_signature = False,deletable=False,details=False)
    return dict(sol=sol)
    #return locals()
def patient():
    #union_table=('Patient','Doctor')
    #temp_db=DAL('sqlite:memory')
    #union_table=temp_db.define_table('union_table',db[union_tables[0]])
    #records=
    return dict(message=T(''))
    
def patientform():
    response.flash = T("Hi Doctor")
    form=SQLFORM(db.Patient)
    if form.process().accepted: #onvalidation=validate
        response.flash='Thank You, Your information Has Been Successfully Submited'
        rows=db(db.Doctor)
        redirect(URL(r=request,f='patientnotification'))
    elif form.errors:
        response.flash='Please Check The Form Again'
    else:
        response.flash='Upload Your Solution'
    return dict(form=form)
    
def patient_doctornotify():
    query=((db.Doctoraccess.Doctor_Request==True))
    fields = (db.Doctoraccess.Doctor_name, db.Doctoraccess.specialisation,db.Doctoraccess.Patient_name, db.Doctoraccess.Patient_Permit)
    sol = SQLFORM.grid(query=query,fields=fields,editable=True,details=False)
    return dict(sol=sol)
def patient_pharmanotify():
    sol = SQLFORM.grid(db.Doctoraccess, showbuttontext=True,user_signature=False)
    return dict(sol=sol)
    
    
def pharmacist():
    #sol = SQLFORM.grid(db.Patient, showbuttontext=True,user_signature=True)
    #return dict(sol=sol)
    return dict(message=T(''))
def pharma_unpermitpatient():
    query=((db.Doctoraccess.Patient_Permit==False)and(db.Doctoraccess.Doctor_Request==False))
    fields = (db.Doctoraccess.Doctor_name,db.Doctoraccess.specialisation, db.Doctoraccess.Patient_name,  db.Doctoraccess.Doctor_Request)
    
    sol = SQLFORM.grid(query=query,fields=fields,user_signature = False,deletable=False,details=False)
    return dict(sol=sol)
def pharma_permitpatient():
    sol=SQLFORM.grid(db.Patient,user_signature = False,deletable=False,details=False)
    return dict(sol=sol)
# ---- Smart Grid (example) -----
@auth.requires_membership('admin') # can only be accessed by members of admin groupd
def grid():
    response.view = 'generic.html' # use a generic view
    tablename = request.args(0)
    if not tablename in db.tables: raise HTTP(403)
    grid = SQLFORM.smartgrid(db[tablename], args=[tablename], deletable=False, editable=False)
    return dict(grid=grid)

    
# ---- Embedded wiki (example) ----
def wiki():
    auth.wikimenu() # add the wiki to the menu
    return auth.wiki() 

# ---- Action for login/register/etc (required for auth) -----
def user():
    """
    exposes:
    http://..../[app]/default/user/login
    http://..../[app]/default/user/logout
    http://..../[app]/default/user/register
    http://..../[app]/default/user/profile
    http://..../[app]/default/user/retrieve_password
    http://..../[app]/default/user/change_password
    http://..../[app]/default/user/bulk_register
    use @auth.requires_login()
        @auth.requires_membership('group name')
        @auth.requires_permission('read','table name',record_id)
    to decorate functions that need access control
    also notice there is http://..../[app]/appadmin/manage/auth to allow administrator to manage users
    """
    return dict(form=auth())

# ---- action to server uploaded static content (required) ---
@cache.action()
def download():
    """
    allows downloading of uploaded files
    http://..../[app]/default/download/[filename]
    """
    return response.download(request, db)
