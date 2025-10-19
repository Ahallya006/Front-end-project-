# Front-end-project-{


"name": "contactformx-demo",

"version": "1.0.0",

"main": "server.js",

"scripts": { "start": "node server.js", "dev": "nodemon server.js" },

"dependencies": {


"cors": "^2.8.5",

"express": "^4.18.2",


"joi": "^17.9.2",

"dotenv": "^16.0.0"

},


"devDependencies": { "nodemon": "^2.0.22" }

}
PORT-5000

MONGO_URI-mongodb+srv://<user>: <pass>@clustero.mongodb.net/contactformx?retryWrites=true&w=majority

ADMIN_EMAIL-admin@example.com

SMTP_HOST=smtp.example.com

SMTP PORT-587

SMTP USER-username
SMTP_PASS-password
/ models/contact.js

const mongoose = require('mongoose');

 const ContactSchema new mongoose.Schema ({

name: { type: String, required: true, trim: true },

email: { type: String, required: true, trim: true },

message: { type: String, required: true },

), { timestamps: true });

module.exports = mongoose.model('Contact', ContactSchema);
router.post('/', async (req, res) => {

 } catch (err) {

 }

 });



 router.get('/', async (req, res) => {

try {

 const items await Contact.find().sort({ createdAt: -1)).limit(100);

res.json(items);

} catch(err) {

 res.status(500).json({ error: 'Server error' });

 }

});
 router.get('/:id', async (req, res) => {

 try {

const item await Contact.findById(req.params.id);

if (!item) return res.status(404).json({ error: 'Not found' });
 res.json(item);

} catch(err) {

res.status(500).json({ error: 'Server error' });

 }

 });
 module.exports = router;
app.post('/api/contact', async (req, res) => {

 try {


const { error, value} = contactSchema.validate(req.body);


if (error) return res.status(400).json({ success: false, error: error.details[0].message });

const contacts = await readContacts();

const newContact = { id: contacts.length + 1, ...value, createdAt: new Date().toISOString() };

contacts.push(newContact);

 await writeContacts (contacts);

// optionally: enqueue email send here

res.status(201).json({ success: true, data: newContact });

 } catch (err) {

console.error(err);

res.status (500).json({ success: false, error: 'Server error' });

 }

});

// List contacts

 app.get('/api/contact', async (req, res) => {

 const contacts = await readContacts();

 res.json(contacts);

});
 const PORT = process.env.PORT || 5000;

app.listen(PORT, ()=> console.log('ContactFormX demo running on $(PORT}`));
body>

<form id="contactForm">
<button>Send</button>

</form>

<pre id="result"></pre>

<script>

const form document.getElementById('contactForm');
form.addEventListener('submit', async (e) => {

e.preventDefault();
const data{

name: form.name.value,

email: form.email.value,
;

message: form.message.value
const res await fetch('/api/contact', {

method: 'POST',

headers: ['Content-Type': 'application/json'},
body: JSON.stringify(data)
});

const json await res.json();

document.getElementById('result').textContent = JSON.stringify(json, null, 2);

});

</script>

</body>

</html>
{success":

true,
 "message": "Contact form submitted successfully"
}
