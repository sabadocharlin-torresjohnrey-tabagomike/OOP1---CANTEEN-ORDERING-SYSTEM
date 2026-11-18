let cartItems = [];
let allOrders = [];
let currentCategory = 'all';

function selectCategory(category, buttonElement) {
    currentCategory = category;

    let buttons = document.querySelectorAll('.category-btn');
    buttons.forEach(btn => btn.classList.remove('active'));
    if (buttonElement) buttonElement.classList.add('active');

    let titleMap = {
        'all': '🍽️ All Menu Items',
        'meals': '🍗 Meals & Main Dishes',
        'sides': '🍚 Extra Rice & Sides',
        'drinks': '🥤 Cold Refreshing Drinks',
        'desserts': '🍮 Sweet Desserts'
    };
    document.getElementById('current-category-title').innerHTML = titleMap[category] || '🍽️ Menu Items';

    let cards = document.getElementsByClassName("item-card");
    for (let i = 0; i < cards.length; i++) {
        let cardCategory = cards[i].getAttribute("data-category");
        if (category === 'all' || cardCategory === category) {
            cards[i].style.display = "flex";
        } else {
            cards[i].style.display = "none";
        }
    }
}

function filterMenu() {
    let input = document.getElementById("searchInput").value.toLowerCase();
    let cards = document.getElementsByClassName("item-card");

    for (let i = 0; i < cards.length; i++) {
        let name = cards[i].getAttribute("data-name");
        let matchesCategory = (currentCategory === 'all' || cards[i].getAttribute("data-category") === currentCategory);

        if (name.includes(input) && matchesCategory) {
            cards[i].style.display = "flex"; 
        } else {
            cards[i].style.display = "none"; 
        }
    }
}

function toggleAdmin() {
    let customerView = document.getElementById("customer-view");
    let adminView = document.getElementById("admin-view");

    if (adminView.classList.contains("hidden") || adminView.style.display === "none" || adminView.style.display === "") {
        let password = prompt("Enter admin password (hint: admin123):");
        if (password !== "admin123") {
            if (password !== null) alert("Incorrect password!");
            return;
        }
        customerView.style.display = "none";
        adminView.classList.remove("hidden");
        adminView.style.display = "block";
        displayAdminOrders();
    } else {
        adminView.style.display = "none";
        adminView.classList.add("hidden");
        customerView.style.display = "block";
    }
}

// ================= FULLY FUNCTIONAL IMAGE PREVIEW MODAL =================
function openProductModal(name, basePrice, image, hasPortion) {
    document.getElementById('modalTitle').innerText = name;
    document.getElementById('modalBasePrice').innerText = '₱' + basePrice;
    document.getElementById('modalImg').src = image;
    document.getElementById('modal-qty').value = 1;

    let portionWrapper = document.getElementById('modalPortionWrapper');
    let portionSelect = document.getElementById('modal-portion');

    if (hasPortion) {
        portionWrapper.style.display = "flex";
        let halfPrice = basePrice / 2;
        portionSelect.innerHTML = `
            <option value="full">Full Portion (₱${basePrice})</option>
            <option value="half">Half Portion (₱${halfPrice % 1 !== 0 ? halfPrice.toFixed(2) : halfPrice})</option>
        `;
    } else {
        portionWrapper.style.display = "none";
    }

    let addBtn = document.getElementById('modalAddBtn');
    addBtn.onclick = function() {
        let qty = parseInt(document.getElementById('modal-qty').value) || 1;
        let portion = hasPortion ? portionSelect.value : 'full';

        let finalPrice = basePrice;
        let itemName = name;

        if (hasPortion && portion === 'half') {
            finalPrice = basePrice / 2;
            itemName += ' (Half Portion)';
        } else if (hasPortion) {
            itemName += ' (Full Portion)';
        }

        let existingItem = cartItems.find(item => item.name === itemName);
        if (existingItem) {
            existingItem.quantity += qty;
        } else {
            cartItems.push({ name: itemName, price: finalPrice, quantity: qty });
        }

        displayCart();

        let originalText = addBtn.innerHTML;
        let originalBg = addBtn.className;
        
        addBtn.className = "w-full bg-green-600 text-white font-black py-3 rounded-2xl shadow-lg transition text-xs sm:text-sm uppercase tracking-wider scale-105";
        addBtn.innerHTML = "✓ Added to Tray!";

        setTimeout(() => {
            addBtn.className = originalBg;
            addBtn.innerHTML = originalText;
            closeProductModal();
        }, 800);
    };

    document.getElementById('productModal').classList.remove('hidden');
}

function closeProductModal() {
    document.getElementById('productModal').classList.add('hidden');
}

// ================= ADD ORDER FROM CARD WITH ✓ ADDED! EFFECT =================
function addOrderFromCard(name, basePrice, portionSelectId, qtyInputId, buttonElement) {
    let portionSelect = document.getElementById(portionSelectId);
    let qtyInput = document.getElementById(qtyInputId);
    
    let portion = portionSelect ? portionSelect.value : 'full';
    let qty = qtyInput ? parseInt(qtyInput.value) : 1;

    if (isNaN(qty) || qty < 1) {
        alert("Pakilagay ng tamang bilang ng order!");
        return;
    }

    let finalPrice = basePrice;
    let itemName = name;

    if (portion === 'half') {
        finalPrice = basePrice / 2;
        itemName += ' (Half Portion)';
    } else {
        itemName += ' (Full Portion)';
    }

    let existingItem = cartItems.find(item => item.name === itemName);
    if (existingItem) {
        existingItem.quantity += qty;
    } else {
        cartItems.push({ name: itemName, price: finalPrice, quantity: qty });
    }

    if (qtyInput) qtyInput.value = 1;
    displayCart();

    let originalText = buttonElement.innerHTML;
    let originalBg = buttonElement.className;
    
    buttonElement.className = "w-full bg-green-600 text-white font-bold py-2 rounded-xl text-[11px] sm:text-xs transition shadow scale-105";
    buttonElement.innerHTML = "✓ Added!";

    setTimeout(() => {
        buttonElement.className = originalBg;
        buttonElement.innerHTML = originalText;
    }, 1000);
}

function addOrderSimple(name, price, qtyInputId, buttonElement) {
    let qtyInput = document.getElementById(qtyInputId);
    let qty = qtyInput ? parseInt(qtyInput.value) : 1;

    if (isNaN(qty) || qty < 1) {
        alert("Pakilagay ng tamang bilang ng order!");
        return;
    }

    let existingItem = cartItems.find(item => item.name === name);
    if (existingItem) {
        existingItem.quantity += qty;
    } else {
        cartItems.push({ name: name, price: price, quantity: qty });
    }

    if (qtyInput) qtyInput.value = 1;
    displayCart();

    let originalText = buttonElement.innerHTML;
    let originalBg = buttonElement.className;
    
    buttonElement.className = "w-full bg-green-600 text-white font-bold py-2 rounded-xl text-[11px] sm:text-xs transition shadow scale-105";
    buttonElement.innerHTML = "✓ Added!";

    setTimeout(() => {
        buttonElement.className = originalBg;
        buttonElement.innerHTML = originalText;
    }, 1000);
}

function changeCartQty(index, change) {
    cartItems[index].quantity += change;
    if (cartItems[index].quantity <= 0) {
        cartItems.splice(index, 1);
    }
    displayCart();
}

function deleteItem(index) {
    cartItems.splice(index, 1);
    displayCart();
}

function displayCart() {
    let tbody = document.getElementById("cart-list");
    tbody.innerHTML = "";

    if (cartItems.length === 0) {
        tbody.innerHTML = `<tr><td colspan="5" class="py-6 sm:py-8 text-center text-gray-400 italic">YOUR TRAY IS EMPTY.<br>I-tap ang "+ Add to Order"!</td></tr>`;
        document.getElementById("total-price").innerText = "0.00";
        return;
    }

    let overallTotal = 0;

    for (let i = 0; i < cartItems.length; i++) {
        let subtotal = cartItems[i].price * cartItems[i].quantity;
        overallTotal += subtotal;

        let row = `<tr class="hover:bg-red-50">
            <td class="py-2 px-1 text-left font-semibold text-gray-800 max-w-[110px] sm:max-w-none break-words">${cartItems[i].name}</td>
            <td class="py-2 px-1 text-center text-gray-600 whitespace-nowrap">₱${cartItems[i].price}</td>
            <td class="py-2 px-1 text-center whitespace-nowrap">
                <button class="bg-gray-200 hover:bg-gray-300 text-gray-800 px-1.5 py-0.5 rounded font-bold text-xs" onclick="changeCartQty(${i}, -1)">-</button>
                <span class="font-bold px-1">${cartItems[i].quantity}</span>
                <button class="bg-gray-200 hover:bg-gray-300 text-gray-800 px-1.5 py-0.5 rounded font-bold text-xs" onclick="changeCartQty(${i}, 1)">+</button>
            </td>
            <td class="py-2 px-1 text-center font-bold text-red-600 whitespace-nowrap">₱${subtotal}</td>
            <td class="py-2 px-1 text-center"><button onclick="deleteItem(${i})" class="bg-red-500 hover:bg-red-600 text-white font-bold py-0.5 px-1.5 sm:px-2 rounded text-xs">✕</button></td>
        </tr>`;

        tbody.innerHTML += row;
    }

    document.getElementById("total-price").innerText = overallTotal.toFixed(2);
}

function checkout() {
    let customerName = document.getElementById("customerName").value.trim();
    if (!customerName) {
        alert("Please enter your Customer Identification Name before placing an order.");
        return;
    }
    if (cartItems.length === 0) {
        alert("Your tray is empty!");
        return;
    }

    let totalAmount = cartItems.reduce((sum, item) => sum + (item.price * item.quantity), 0);
    let orderSummary = cartItems.map(item => `${item.quantity}x ${item.name}`).join(", ");

    allOrders.push({
        id: allOrders.length + 1,
        customer: customerName,
        items: orderSummary,
        total: totalAmount
    });

    alert("Order placed successfully! Thank you, " + customerName + "!");
    cartItems = []; 
    document.getElementById("customerName").value = "";
    displayCart();
}

function displayAdminOrders() {
    let tbody = document.getElementById("admin-order-list");
    tbody.innerHTML = "";

    let pendingCountElem = document.getElementById("admin-pending-count");
    if (pendingCountElem) {
        pendingCountElem.innerText = allOrders.length;
    }

    if (allOrders.length === 0) {
        tbody.innerHTML = `<tr><td colspan="5" style="text-align: center; color: #777; padding: 20px;">No active customer orders yet.</td></tr>`;
        return;
    }

    for (let i = 0; i < allOrders.length; i++) {
        let order = allOrders[i];
        let row = `<tr class="hover:bg-red-50/50">
            <td class="py-3 px-3 sm:px-4 font-extrabold text-red-600">#${order.id}</td>
            <td class="py-3 px-3 sm:px-4 font-semibold text-gray-800">${order.customer}</td>
            <td class="py-3 px-3 sm:px-4 text-left font-medium">${order.items}</td>
            <td class="py-3 px-3 sm:px-4 text-center font-bold text-gray-800">₱${order.total.toFixed(2)}</td>
            <td class="py-3 px-3 sm:px-4 text-center"><button onclick="completeOrder(${i})" class="bg-green-600 hover:bg-green-700 text-white px-3 py-1.5 rounded-lg text-xs font-bold transition shadow whitespace-nowrap">Complete / Clear</button></td>
        </tr>`;
        tbody.innerHTML += row;
    }
}

function completeOrder(index) {
    allOrders.splice(index, 1);
    displayAdminOrders();
}