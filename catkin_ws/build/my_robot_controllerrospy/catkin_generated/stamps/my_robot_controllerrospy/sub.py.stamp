#!/usr/bin/env python3
import rospy
from std_msgs.msg import String,Int32,Float64
from geometry_msgs.msg import Twist
from threading import Thread
import time
def callback_line(data):
    rospy.loginfo("line: %d\n" % (data.data))
def callback_total_distance(data):
    rospy.loginfo("total distance %f\n" % (data.data))
def callback_velocity(data):
    rospy.loginfo("x: %f, y: %f\n" % (data.linear.x, data.linear.y))
def line_sub():
    rospy.Subscriber("line", Int32, callback_line)
    time.sleep(0.25)
    rospy.spin()
def total_distance_sub():
    rospy.Subscriber("total_distance", Float64, callback_total_distance)
    time.sleep(0.25)
    rospy.spin()
def velocity_sub():
    rospy.Subscriber("/cmd_vel", Twist, callback_velocity)
    time.sleep(0.25)
    rospy.spin()

if __name__ == '__main__':
    rospy.init_node('data_sub', anonymous=True)
    f1 = Thread(target=line_sub)
    f2 = Thread(target=total_distance_sub)
    f3 = Thread(target=velocity_sub)
    try:
        f1.start()
        f2.start()
        f3.start()
    except rospy.ROSInterruptException:
        pass