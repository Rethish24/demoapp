import streamlit as st
import pandas as pd
import os

# Initial bike data
base_bikes = pd.DataFrame([
    # Existing entries like Pulsar, Classic 350, R15, etc.
    # (Refer to earlier code block)
])

# Additional brands and models
additional_bikes = pd.DataFrame([
    {
        "Model": "Honda CB350 H'ness",
        "Price": 209857,
        "Type": "Cruiser",
        "Brand": "Honda",
        "Link": "https://www.honda2wheelersindia.com/motorcycle/cb350-hness",
        "Engine": "348.36cc",
        "Power": "20.8 bhp",
        "Torque": "30 Nm",
        "Mileage": "45 km/l",
        "Seat Height": "800 mm",
        "Weight": "181 kg",
        "Maintenance": "₹3,000–₹4,000/year",
        "Comfort": "Classic cruiser with comfortable seating and upright posture."
    },
    {
        "Model": "TVS Ronin",
        "Price": 149000,
        "Type": "Cruiser",
        "Brand": "TVS",
        "Link": "https://www.tvsmotor.com/tvs-ronin",
        "Engine": "225.9cc",
        "Power": "20.4 PS",
        "Torque": "19.93 Nm",
        "Mileage": "40 km/l",
        "Seat Height": "795 mm",
        "Weight": "160 kg",
        "Maintenance": "₹3,500–₹4,500/year",
        "Comfort": "Versatile bike suitable for both city rides and long tours."
    },
    {
        "Model": "Triumph Speed 400",
        "Price": 234000,
        "Type": "Roadster",
        "Brand": "Triumph",
        "Link": "https://www.triumphmotorcycles.in/motorcycles/roadsters/speed-400",
        "Engine": "398.15cc",
        "Power": "39.5 bhp",
        "Torque": "37.5 Nm",
        "Mileage": "30 km/l",
        "Seat Height": "790 mm",
        "Weight": "170 kg",
        "Maintenance": "₹6,000–₹8,000/year",
        "Comfort": "Modern roadster with agile handling and comfortable ergonomics."
    },
    {
        "Model": "Benelli TRK 502X",
        "Price": 620000,
        "Type": "Adventure",
        "Brand": "Benelli",
        "Link": "https://www.benelli.com/in-en/product/trk-502x",
        "Engine": "500cc",
        "Power": "47.5 PS",
        "Torque": "46 Nm",
        "Mileage": "25 km/l",
        "Seat Height": "840 mm",
        "Weight": "235 kg",
        "Maintenance": "₹7,000–₹9,000/year",
        "Comfort": "Adventure tourer designed for long-distance comfort and off-road capability."
    }
])

# Merge all bikes
df = pd.concat([base_bikes, additional_bikes], ignore_index=True)

# Initialize reviews
df["Reviews"] = [[] for _ in range(len(df))]
if "reviews" not in st.session_state:
    st.session_state.reviews = {model: [] for model in df["Model"]}

# UI
st.title("🏍️ Bike Recommendation App")

budget = st.slider("Select your budget (in ₹)", 50000, 700000, 200000, step=5000)
usage = st.selectbox("Preferred Usage Type", df["Type"].unique())
brand = st.multiselect("Preferred Brands", df["Brand"].unique(), default=df["Brand"].unique())

# Filter bikes
filtered = df[(df["Price"] <= budget) & (df["Type"] == usage) & (df["Brand"].isin(brand))]

st.subheader("🔍 Recommended Bikes")
if not filtered.empty:
    for idx, row in filtered.iterrows():
        with st.expander(f"{row['Model']} (₹{row['Price']})"):
            # Display image
            image_file = row['Model'].lower().replace(" ", "").replace("'", "").replace("-", "") + ".jpg"
            image_path = os.path.join("images", image_file)
            if os.path.exists(image_path):
                st.image(image_path, width=300)
            else:
                st.info("Image not available.")

            st.markdown(f"[Official Site]({row['Link']})")
            st.markdown(f"**Brand**: {row['Brand']}")
            st.markdown(f"**Type**: {row['Type']}")

            st.markdown("### 🛠️ Specifications")
            st.markdown(f"- Engine: {row['Engine']}")
            st.markdown(f"- Power: {row['Power']}")
            st.markdown(f"- Torque: {row['Torque']}")
            st.markdown(f"- Mileage: {row['Mileage']}")
            st.markdown(f"- Seat Height: {row['Seat Height']}")
            st.markdown(f"- Weight: {row['Weight']}")

            st.markdown("### 💰 Maintenance & Comfort")
            st.markdown(f"- Maintenance: {row['Maintenance']}")
            st.markdown(f"- Comfort: {row['Comfort']}")

            st.markdown("### 📝 User Reviews")
            for review in st.session_state.reviews[row['Model']]:
                st.markdown(f"> ⭐ {review['rating']} - *{review['name']}*: {review['review']}")
            if not st.session_state.reviews[row['Model']]:
                st.info("No reviews yet.")

            with st.form(f"form_{idx}"):
                name = st.text_input("Name", key=f"name_{idx}")
                rating = st.slider("Rating", 1, 5, key=f"rating_{idx}")
                comment = st.text_area("Your Review", key=f"review_{idx}")
                if st.form_submit_button("Submit"):
                    if name and comment:
                        st.session_state.reviews[row['Model']].append({
                            "name": name,
                            "rating": rating,
                            "review": comment
                        })
                        st.success("Review submitted!")
                        st.experimental_rerun()
else:
    st.warning("No bikes match your selected criteria.")
