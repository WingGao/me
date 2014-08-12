---
layout: post
title: Python Behavior Tree Example
category: Tech
tags: [python, AI]
comments: true
---

Use [owyl](https://github.com/eykd/owyl)
	
	# coding=utf-8
	__author__ = 'Wing'
	import owyl
	from owyl import blackboard
	
	
	class Friend():
	    def __init__(self, backboard):
	        self.bb = backboard
	
	        self.tree = self.buildTree()
	
	    def do(self):
	        [i for i in self.tree]
	
	    def buildTree(self):
	        tree = owyl.sequence(
	            # 学习
	            owyl.sequence(
	                self.isRestDay(),
	                owyl.sequence(
	                    self.isDayExpNotMax(),
	                    self.isDayNumNotMax(),
	                    self.study()
	                ),
	                self.setNextStudyTime()
	            ),
	            # 社交
	            owyl.sequence(
	                # 赞
	                owyl.selector(
	                    owyl.sequence(
	                        self.canLike(),
	                        owyl.selector(
	                            owyl.sequence(
	                                self.isOppSex(),
	                                self.sendLike(is_opp_sex=True)
	                            ),
	                            self.sendReminder(is_opp_sex=False)
	                        )
	                    ),
	                    self.nothing()
	                ),
	                # 提醒
	                owyl.selector(
	                    owyl.sequence(
	                        self.canReminder(),
	                        owyl.selector(
	                            owyl.sequence(
	                                self.isOppSex(),
	                                self.sendReminder(is_opp_sex=True)
	                            ),
	                            self.sendReminder(is_opp_sex=False)
	                        )
	                    ),
	                    self.nothing()
	                )
	            )
	        )
	        return owyl.visit(tree)
	
	    @owyl.taskmethod
	    def isRestDay(self, **kwargs):
	        yield True
	
	    @owyl.taskmethod
	    def isDayExpNotMax(self, **kwargs):
	        yield True
	
	    @owyl.taskmethod
	    def isDayNumNotMax(self, **kwargs):
	        yield True
	
	    @owyl.taskmethod
	    def isRestDay(self, **kwargs):
	        yield True
	
	    @owyl.taskmethod
	    def study(self, **kwargs):
	        print 'studying'
	        yield True
	
	    @owyl.taskmethod
	    def setNextStudyTime(self, **kwargs):
	        print 'setNextStudyTime'
	        yield True
	
	    @owyl.taskmethod
	    def canLike(self, **kwargs):
	        yield True
	
	    @owyl.taskmethod
	    def isOppSex(self, **kwargs):
	        yield True
	
	    @owyl.taskmethod
	    def sendLike(self, **kwargs):
	        """Like action
	
	        :param is_opp_sex: is opp sex
	        """
	        isOppSex = kwargs['is_opp_sex']
	        print 'like %r' % isOppSex
	        yield True
	
	    @owyl.taskmethod
	    def canReminder(self, **kwargs):
	        yield True
	
	
	    @owyl.taskmethod
	    def sendReminder(self, **kwargs):
	        """Reminder action
	
	        :param is_opp_sex: is opp sex
	        """
	        is_opp_sex = kwargs['is_opp_sex']
	        print 'reminder %r' % is_opp_sex
	        yield True
	
	
	    @owyl.taskmethod
	    def nothing(self, **kwargs):
	        yield True
	
	
	    @owyl.taskmethod
	    def stay(self, **kwargs):
	        print 'stay'
	        yield True
	
	
	if __name__ == '__main__':
	    bb = blackboard.Blackboard()
	    f = Friend(bb)
	    f.do()

	
	
