# mjshop
mjshop
code: generateCode(),
region: document.getElementById('accountRegion').value,
email: document.getElementById('accountEmail').value,
password: document.getElementById('accountPassword').value,
inGameName: document.getElementById('inGameName').value,
mobile: document.getElementById('mobileNumber').value,
timestamp: new Date().toISOString()
};
orders.push(newOrder);
saveOrders(); // Save the updated orders array

// Display generated code
document.getElementById('generatedCodeDisplay').textContent = newOrder.code;
hideModal('orderFormModal');
showModal('orderCompleteModal');

// Clear form fields
document.getElementById('orderForm').reset();
});

// Admin Button logic
document.getElementById('adminBtn').addEventListener('click', () => {
console.log('Admin button clicked!'); // Debugging hint
showModal('adminLoginModal');
});

// Admin Login logic
document.getElementById('adminLoginForm').addEventListener('submit', (e) => {
e.preventDefault();
const password = document.getElementById('adminPassword').value;
if (password === '1315') { // Hardcoded password
hideModal('adminLoginModal');
showModal('adminPanelModal');
document.getElementById('adminPassword').value = ''; // Clear password field
} else {
alert('رمز عبور اشتباه است!');
}
});

// Admin Panel Code Lookup logic
document.getElementById('lookupCodeForm').addEventListener('submit', (e) => {
e.preventDefault();
const codeToLookup = document.getElementById('adminLookupCode').value.trim();
const foundOrder = orders.find(order => order.code === codeToLookup);
const resultDiv = document.getElementById('lookupResult');

if (foundOrder) {
resultDiv.innerHTML = `
<p><strong>ریجن اکانت:</strong> ${foundOrder.region}</p>
<p><strong>ایمیل اکانت:</strong> ${foundOrder.email}</p>
<p><strong>پسورد اکانت:</strong> ${foundOrder.password}</p>
<p><strong>اسم داخل بازی:</strong> ${foundOrder.inGameName}</p>
<p><strong>شماره موبایل:</strong> ${foundOrder.mobile}</p>
<p><strong>زمان ثبت:</strong> ${new Date(foundOrder.timestamp).toLocaleString('fa-IR')}</p>
`;
} else {
resultDiv.innerHTML = `<p style="color: red;">کد یافت نشد.</p>`;
}
document.getElementById('adminLookupCode').value = ''; // Clear input field
});

// Close buttons for all modals
document.querySelectorAll('.close-modal').forEach(btn => {
btn.addEventListener('click', () => {
console.log('Close button clicked!'); // Debugging hint
// Find the closest parent with class 'custom-modal'
const modalElement = btn.closest('.custom-modal'); // Changed from .modal
if (modalElement) {
hideModal(modalElement.id);
}
});
});
</script>
</body>
</html>
