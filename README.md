# Number-of-People-Aware-of-a-Secret

On day 1, one person discovers a secret.

You are given an integer delay, which means that each person will share the secret with a new person every day, starting from delay days after discovering the secret. You are also given an integer forget, which means that each person will forget the secret forget days after discovering it. A person cannot share the secret on the same day they forgot it, or on any day afterwards.

Given an integer n, return the number of people who know the secret at the end of day n. Since the answer may be very large, return it modulo 109 + 7.

class Solution(object):
    def peopleAwareOfSecret(self, n, delay, forget):
        MOD = 10**9 + 7
        share = 0
        dp = [0]*n
        dp[0] = 1
        for i in range(1, n):
            if i - delay >= 0:
                share =  (share + dp[i - delay]) % MOD
            if i - forget >= 0:
                share = ( share - dp[i - forget] ) % MOD
            dp[i] = share
        res = 0
        for i in range(n - forget, n):
            if i >= 0:
              res = (res + dp[i]) % MOD
        return res
