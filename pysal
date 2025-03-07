import matplotlib.pyplot as plt
import numpy as np
import geopandas as gpd
from seaborn import kdeplot
from libpysal.weights.contiguity import Queen
from esda.moran import Moran, Moran_Local
from splot.esda import moran_scatterplot, lisa_cluster
from pointpats import PointPattern
from pointpats.centrography import mean_center, ellipse, std_distance
from matplotlib.patches import Ellipse

# Load the dataset
cholera_hex = gpd.read_file('cholera_deaths_hexagons.shp')
cholera_points = gpd.read_file('Cholera_Deaths.shp')
pump_loc = gpd.read_file('Pumps.shp')

# Global Moran's I
y = cholera_hex['death'].values
w = Queen.from_dataframe(cholera_hex)
w.transform = 'r'
moran = Moran(y, w)
print(f"Global Moran's I: {moran.I}")

# Moran's I Scatterplot
fig, ax = moran_scatterplot(moran, aspect_equal=True)
plt.show()

# Local Moran's I
moran_loc = Moran_Local(y, w)
fig, ax = moran_scatterplot(moran_loc)
ax.set_xlabel('Deaths')
ax.set_ylabel('Spatial Lag of Deaths')
plt.show()

# Standard Distance Circle
coord_list = [(x, y) for x, y in zip(cholera_points.geometry.x, cholera_points.geometry.y)]
pp = PointPattern(coord_list)
mc = mean_center(pp.points)
stdd = std_distance(pp.points)

fig, ax = plt.subplots()
ax.set_aspect('equal')
circle = plt.Circle((mc[0], mc[1]), stdd, color='r', fill=False)
ax = pp.plot(get_ax=True, title='Standard Distance Circle')
ax.add_artist(circle)
plt.plot(mc[0], mc[1], 'y^', label='Mean Center')
plt.legend()
plt.show()

# Standard Deviational Ellipse
major, minor, rotation = ellipse(pp.points)
theta_degree = np.degrees(rotation)
e = Ellipse(xy=mc, width=major*2, height=minor*2, angle=-theta_degree,
            facecolor='none', edgecolor='green', linestyle='--', linewidth=3, label='Std.Ellipse')

fig, ax = plt.subplots()
ax.set_aspect('equal')
cholera_points.plot(ax=ax, color='navy', markersize=5, label='Cholera Deaths')
pump_loc.plot(ax=ax, marker='s', color='red', markersize=12, label='Water Pump')
ax.add_patch(e)
plt.plot(mc[0], mc[1], color='orange', marker='X', label='Mean Center')
plt.legend()
plt.title('Standard Deviational Ellipse')
plt.show()

# Kernel Density Estimation (KDE)
cholera_count = cholera_points['Count']
fig, ax = plt.subplots(figsize=(7, 7))
kdeplot(x=cholera_points.geometry.x, y=cholera_points.geometry.y,
        weights=cholera_count, levels=30, cmap='viridis_r', label='Kernel Density Estimation')
cholera_points.plot(ax=ax, color='navy', markersize=5, label='Cholera Deaths')
pump_loc.plot(ax=ax, marker='s', color='red', markersize=12, label='Water Pump')
plt.legend()
plt.title('Kernel Density Estimation')
plt.show()
