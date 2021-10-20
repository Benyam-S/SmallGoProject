# SmallGoProject

Required entities

type Admin struct {
	ID          string
	FirstName   string
	LastName    string
	Country     string
	Email       string
	Role        string // distinguesh super-admin from admin
  APIKey      string
	CreatedAt   time.Time
	UpdatedAt   time.Time
}

type User struct {
	ID            string
	FirstName     string
	LastName      string
	Country       string
	Email         string
	Nickname      string
  Phonenumber   string
  SlackUsername string
	CreatedAt     time.Time
	UpdatedAt     time.Time
}

type Notification struct {
	ID              string
	Title           string
	Description     string
  Destination     string
  NotifyAt        time.Time  // Updated every time after successful notification
  Frequency       int64 // The frequency gap in seconds
  AcknowledgeLink string
  AuthenticatedBy string
	CreatedAt       time.Time
	UpdatedAt       time.Time
}


Required endpoints


* Admin Requests
 - All admin requests must include API key in the request header
 - The super-admin credentials will be read from the environment file
 - Another admin credentials will be read from the database

----------------------------------------------- ADMIN CRUD -----------------------------------------------
/admin/admin  [POST]
- Using this endpoint super admin is able to create new admin
- The super admin sends an admin entity described as above in json format
- The system will accept this request and add it to the database after making necessary validation of the data

/admin/admin/{id}  [PUT]
- Using this endpoint super admin is able to update admin entity that matches the provided id in the request

/admin/admin/{id}  [GET]
- Using this endpoint super admin is able to view another admin entity that matches the provided id in the request

/admin/admin/{id}  [DELETE]
- Using this endpoint super admin is able to delete another admin entity that matches the provided id in the request


----------------------------------------------- USER CRUD -----------------------------------------------
/admin/user       [POST]
- Using this endpoint admin is able to create new users
- The admin sends an user entity described as above in json format
- The system will accept this request and add it to the database after making necessary validation of the data

/admin/user/{id}  [PUT]
- Using this endpoint admin is able to update user entity that matches the provided id in the request

/admin/user/{id}  [GET]
- Using this endpoint admin is able to view user entity that matches the provided id in the request

/admin/users  [GET]
- Using this endpoint admin is able to view one or more user entities
- The request contain a search form for matching one or more user entities

/admin/user/{id}  [DELETE]
- Using this endpoint admin is able to delete user entity that matches the provided id in the request


----------------------------------------------- Notification CRUD -----------------------------------------------
/admin/notification       [POST]
- Using this endpoint admin is able to create new notification request
- The admin sends an notification entity described as above in json format
- The system will accept this request and add it to the database after making necessary validation of the data

/admin/notification/{id}  [PUT]
- Using this endpoint admin is able to update notification entity that matches the provided id in the request

/admin/notification/{id}  [GET]
- Using this endpoint admin is able to view notification entity that matches the provided id in the request

/admin/notification/{id}  [DELETE]
- Using this endpoint admin is able to delete notification entity that matches the provided id in the request


/notification/acknowledge/{id} [POST]
- Using this endpoint user or admin can pause or stop further sending of notifications
- id refers to the ID of the notification
- id can also be a generated serial number that can be saved with the notification entity
