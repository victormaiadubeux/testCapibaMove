import streamlit as st
import pandas as pd
import numpy as np
import folium
import geopy.distance
import time

# Sample data for boat spots along the Capibaribe River
boat_spots_data = {
    'Name': ['Marco Zero', 'Recife Antigo', 'Cais da Alfândega'],
    'LATITUDE': [-8.063229, -8.063372, -8.063989],  # Updated latitude for Recife
    'LONGITUDE': [-34.871479, -34.873842, -34.873343]   # Updated longitude for Recife
}

boat_spots_df = pd.DataFrame(boat_spots_data)

# Streamlit app layout
st.title('River Boat Transportation Service in Recife')

# Display boat spots on a map
st.subheader('Available Boat Spots')
m = folium.Map(location=[-8.0636, -34.8714], zoom_start=15)  # Centered around Recife
for index, row in boat_spots_df.iterrows():
    folium.Marker([row['LATITUDE'], row['LONGITUDE']], popup=row['Name']).add_to(m)
st.write(m)

# User input for pickup and drop-off spots
pickup_spot = st.selectbox('Select Pickup Spot:', boat_spots_df['Name'])
dropoff_spot = st.selectbox('Select Drop-off Spot:', boat_spots_df['Name'])

# Function to calculate the distance between two spots
def calculate_distance(pickup, dropoff):
    pickup_coords = boat_spots_df.loc[boat_spots_df['Name'] == pickup, ['LATITUDE', 'LONGITUDE']].values[0]
    dropoff_coords = boat_spots_df.loc[boat_spots_df['Name'] == dropoff, ['LATITUDE', 'LONGITUDE']].values[0]
    return geopy.distance.geodesic(pickup_coords, dropoff_coords).kilometers

# Calculate distance and fare estimation
distance = calculate_distance(pickup_spot, dropoff_spot)
fare_estimation = 20 + 5 * distance  # Base fare plus 5 currency units per kilometer

# Display fare estimation to the user
st.subheader('Fare Estimation')
st.write(f"Distance between {pickup_spot} and {dropoff_spot}: {distance:.2f} kilometers")
st.write(f"Estimated fare: {fare_estimation:.2f} currency units")

# Request for boat service button
if st.button('Request Boat Service'):
    # Simulate boat movement
    st.success('Your boat service request has been sent! A boat will pick you up shortly.')
    time.sleep(3)  # Simulate boat arrival
    st.info('The boat is on its way to pick you up.')
    time.sleep(3)  # Simulate boat arrival
    st.info('You have been picked up! Enjoy your ride.')
    time.sleep(3)  # Simulate boat ride
    st.info('You have arrived at your destination. Thank you for using our service!')
