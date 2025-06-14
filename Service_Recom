import streamlit as st
from datetime import date

st.title("🚘 Car Service Advisor with Issue Analysis")

# 1️⃣ Owner & car details
owner_name = st.text_input("Owner Name")
phone_number = st.text_input("Phone Number")

car_make = st.text_input("Car Make (e.g., Toyota, Hyundai)")
car_model = st.text_input("Car Model (e.g., Innova, i20)")
registration_number = st.text_input("Registration Number")
car_age = st.number_input("Car Age (years)", min_value=0, step=1)
mileage = st.number_input("Total KMs Driven", min_value=0, step=500)
kms_since_service = st.number_input("KMs Driven Since Last Service", min_value=0, step=500)
last_service_date = st.date_input("Last Service Date", value=date.today())

complaints = st.text_area("Any major complaints about the car? (e.g., brake noise, AC not cooling, unusual noise)")

st.markdown("---")

# 2️⃣ Optional add-ons
st.write("### 🧼 Optional Add-on Services (Select as needed)")
add_interior_cleaning = st.checkbox("✅ Deep Interior Cleaning (₹1500)")
add_ceramic_coating = st.checkbox("✅ Ceramic Coating (₹10000)")
add_headlight_polish = st.checkbox("✅ Headlight Polishing (₹800)")
add_tyres_alignment = st.checkbox("✅ Tyre Alignment & Balancing (₹1200)")

if st.button("Generate Service Package"):
    service_items = []
    core_cost = 0
    addons_cost = 0
    issues_found = []

    # Core services
    if kms_since_service >= 10000:
        service_items.append({'task': 'General service + engine oil change', 'cost': 2500})
        core_cost += 2500
    if kms_since_service >= 20000 or car_age >= 2:
        service_items.append({'task': 'Replace air and oil filters', 'cost': 1200})
        core_cost += 1200
    if mileage >= 50000:
        service_items.append({'task': 'Transmission oil change', 'cost': 2500})
        core_cost += 2500

    # Complaint-based diagnosis
    complaint_text = complaints.lower()

    if "brake" in complaint_text:
        issues_found.append({
            'problem': "Brake noise / poor braking",
            'reason': "Brake pads worn or brake disc issues",
            'fix': "Brake pad replacement + disc inspection",
            'cost': 3000
        })
        core_cost += 3000

    if "ac" in complaint_text or "a/c" in complaint_text:
        issues_found.append({
            'problem': "AC not cooling",
            'reason': "Low refrigerant gas or clogged filter",
            'fix': "AC gas refill + filter cleaning",
            'cost': 2000
        })
        core_cost += 2000

    if "noise" in complaint_text:
        issues_found.append({
            'problem': "Unusual noise from suspension",
            'reason': "Worn suspension bushes or components",
            'fix': "Suspension inspection + component replacement if needed",
            'cost': 1500
        })
        core_cost += 1500

    if "engine" in complaint_text:
        issues_found.append({
            'problem': "Engine performance issue",
            'reason': "Possible spark plug or injector problem",
            'fix': "Engine tuning + injector cleaning",
            'cost': 2500
        })
        core_cost += 2500

    # Always general check-up
    service_items.append({'task': 'General car health check-up', 'cost': 500})
    core_cost += 500

    # Add-ons
    if add_interior_cleaning:
        service_items.append({'task': 'Deep interior cleaning', 'cost': 1500})
        addons_cost += 1500
    if add_ceramic_coating:
        service_items.append({'task': 'Ceramic coating', 'cost': 10000})
        addons_cost += 10000
    if add_headlight_polish:
        service_items.append({'task': 'Headlight polishing', 'cost': 800})
        addons_cost += 800
    if add_tyres_alignment:
        service_items.append({'task': 'Tyre alignment & balancing', 'cost': 1200})
        addons_cost += 1200

    total_cost = core_cost + addons_cost

    # 3️⃣ Show the result
    st.success("✅ Service Package Generated with Issue Analysis")

    st.write("### 👤 Owner & Car Info")
    st.write(f"**Owner:** {owner_name}")
    st.write(f"**Phone:** {phone_number}")
    st.write(f"**Car:** {car_make} {car_model} | Reg: {registration_number}")
    st.write(f"**Car Age:** {car_age} years | **KM Driven:** {mileage}")
    st.write(f"**KM Since Last Service:** {kms_since_service} | **Last Service:** {last_service_date}")
    st.write(f"**Complaints:** {complaints if complaints else 'None'}")

    st.write("### 🔍 Identified Issues & Fixes")
    if issues_found:
        for issue in issues_found:
            st.write(f"- **Problem:** {issue['problem']}")
            st.write(f"  - **Reason:** {issue['reason']}")
            st.write(f"  - **Fix Needed:** {issue['fix']} (₹{issue['cost']})")
    else:
        st.write("No specific issues detected from complaints. General service recommended.")

    st.write("### 🛠 Core Service Items")
    for item in service_items:
        if item['task'] in [
            'Deep interior cleaning', 'Ceramic coating',
            'Headlight polishing', 'Tyre alignment & balancing'
        ]:
            continue
        st.write(f"- {item['task']} (₹{item['cost']})")
    st.write(f"💰 **Core Package Cost:** ₹{core_cost}")

    if addons_cost > 0:
        st.write("### ✨ Selected Add-ons")
        for item in service_items:
            if item['task'] in [
                'Deep interior cleaning', 'Ceramic coating',
                'Headlight polishing', 'Tyre alignment & balancing'
            ]:
                st.write(f"- {item['task']} (₹{item['cost']})")
        st.write(f"💰 **Add-ons Cost:** ₹{addons_cost}")

    st.markdown(f"### 🚀 **Total Package Cost: ₹{total_cost}**")
