# Leetcode----3443
Maximum Manhattan Distance After K Changes
//code in java 
class Solution {
    public int maxDistance(String s, int k) {
        // Calculate maximum distance for each dominant direction
        int ne = calculateMaxDistance(s, k, 'N', 'E');
        int nw = calculateMaxDistance(s, k, 'N', 'W');
        int se = calculateMaxDistance(s, k, 'S', 'E');
        int sw = calculateMaxDistance(s, k, 'S', 'W');

        // Return the overall maximum
        return Math.max(Math.max(ne, nw), Math.max(se, sw));
    }

    private int calculateMaxDistance(String s, int k, char primaryDir1, char primaryDir2) {
        int maxDist = 0;
        int currentPos = 0; // Represents the "score" in the dominant direction
        int changesUsed = 0; // Counts changes made to unfavorable characters

        for (char c : s.toCharArray()) {
            if (c == primaryDir1 || c == primaryDir2) {
                currentPos++; // Character aligns with dominant direction
            } else if (changesUsed < k) {
                currentPos++; // Character is opposite but can be changed
                changesUsed++;
            } else {
                currentPos--; // Character is opposite and no changes left
            }
            maxDist = Math.max(maxDist, currentPos); // Update max distance
        }
        return maxDist;
    }
}
