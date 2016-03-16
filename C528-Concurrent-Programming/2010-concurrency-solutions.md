TEA_ROBOT = (sugar_please[i:1..3] -> SUGAR[i]),
SUGAR[i:1..3] = (when i > 1 sugar -> SUGAR[i-1]
				|when i == 1 sugar -> TEA_ROBOT).
				
				
