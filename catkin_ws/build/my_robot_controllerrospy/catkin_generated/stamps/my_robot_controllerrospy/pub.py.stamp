#!/usr/bin/env python3
import rospy
from std_msgs.msg import Float64, Int32
from geometry_msgs.msg import Twist
from timeit import default_timer
from threading import Thread
import time
total_distance = 0.0
line = 0
velocity = Twist()
velocity.linear.x = 0
velocity.linear.y = 0
velocity.linear.z = 0
velocity.angular.x = 0
velocity.angular.y = 0
velocity.angular.z = 0    
def total_distance_pub():
    pub = rospy.Publisher('total_distance', Float64, queue_size=10)
    pub.publish(total_distance)
    rospy.loginfo("%d total distance published.\n" % total_distance)
def line_pub():
    pub = rospy.Publisher('line', Int32, queue_size=10)
    pub.publish(line)
    rospy.loginfo("line is published.\n")
def velocity_pub():
    pub = rospy.Publisher('/cmd_vel', Twist, queue_size=10)
    pub.publish(velocity)
    rospy.loginfo("velocity published.\n")
def simulate():
    start = default_timer()
    while not rospy.is_shutdown():
        total_distance = (default_timer() - start) * 2
        total_mod = total_distance % 140
        if total_mod < 20:
            line = 1
            velocity.linear.y = 2
            velocity.linear.x = 0
        elif total_mod < 30:
            line = 2
            velocity.linear.y = 0
            velocity.linear.x = 2
        elif total_mod < 50:
            line = 2
            velocity.linear.y = -2
            velocity.linear.x = 0
        elif total_mod < 60:
            line = 3
            velocity.linear.y = 0
            velocity.linear.x = 2
        elif total_mod < 80:
            line = 3
            velocity.linear.y = 2
            velocity.linear.x = 0
        elif total_mod < 90:
            line = 4
            velocity.linear.y = 0
            velocity.linear.x = 2
        elif total_mod < 110:
            line = 4
            velocity.linear.y = -2
            velocity.linear.x = 0
        elif total_mod < 120:
            line = 5
            velocity.linear.y = 0
            velocity.linear.x = 2
        else:
            line = 5
            velocity.linear.y = 2
            velocity.linear.x = 0
        total_distance_pub()
        line_pub()
        velocity_pub()
        time.sleep(0.25)
if __name__ == '__main__':
    rospy.init_node("data_pub",anonymous=True)
    try:
        simulate()
    except rospy.ROSInterruptException:
        pass