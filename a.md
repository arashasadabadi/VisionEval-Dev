/*

 * PerType	Description							PerType8			ESR				WKHP 		SCHG		Age  		Major Univ Student  		On Campus

 * -------	----------------------------------	------------------	--------------	-----------	-----------	----------	-----------

 * 1.1.1	ft-worker,20+						FT_WORKER			{ 1, 2, 4, 5 }	[35, 999]	{0,4,5}		[20, 999]	FALSE, FALSE

 * 1.1.2	ft-worker,16-19						FT_WORKER			{ 1, 2, 4, 5 }	[35, 999]	{0}			[16, 19]	FALSE, FALSE

 * 1.2		ft-worker,student					FT_WORKER			{ 1, 2, 4, 5 }	[35, 999]	{6,7}		[16, 999]	FALSE, FALSE

 * 2.1.1	pt-worker,20+						PT_WORKER			{ 1, 2, 4, 5 }	[0, 34]		{0,4,5}		[20, 999]	FALSE, FALSE

 * 2.1.2	pt-worker,16-19						PT_WORKER			{ 1, 2, 4, 5 }	[0, 34]		{0}			[16, 19]	FALSE, FALSE

 * 2.2.1	pt-worker,student,21-34 hours		PT_WORKER			{ 1, 2, 4, 5 }	[21, 34]	{6,7}		[16, 999]	FALSE, FALSE

 * 2.2.2	pt-worker,student,0-20 hours		PT_WORKER			{ 1, 2, 4, 5 }	[0, 20]		{6,7}		[35, 999]	FALSE, FALSE

 * 3.1.1	univ student,major,non-worker		UNIV_STUDENT		{ 0, 3, 6 }		[0, 999]	{6,7}		[15, 99]	TRUE, FALSE

 * 3.1.2	univ student,OTHER,non-worker		UNIV_STUDENT		{ 0, 3, 6 }		[0, 999]	{6,7}		[16, 64]	FALSE, FALSE

 * 3.2.1.1	univ student,major,worker,on-campus	UNIV_STUDENT		{ 1, 2, 4, 5 }	[0, 999]	{6,7}		[15, 99]	TRUE, TRUE

 * 3.2.1.2	univ student,major,worker,off-campus	UNIV_STUDENT		{ 1, 2, 4, 5 }	[0, 999]	{6,7}		[15, 99]	TRUE, FALSE

 * 3.2.2	univ student,OTHER,worker			UNIV_STUDENT		{ 1, 2, 4, 5 }	[0, 20]		{6,7}		[16, 34]	FALSE, FALSE

 * 4.1		non-worker homemaker,17-64,schg=0	NON_WORKING_ADULT	{ 0, 3, 6 }		[0, 999]	{0}			[17, 64]	FALSE, FALSE

 * 4.2		non-worker homemaker,17-64,schg=4,5	NON_WORKING_ADULT	{ 0, 3, 6 }		[0, 999]	{4,5}		[20, 64]	FALSE, FALSE

 * 5		retired								RETIREE				{ 0, 3, 6 }		[0, 999]	{0,4-7}		[65, 99]	FALSE, FALSE

 * 6.1.1	driving age,worker,16-19			DRIVING_STUDENT		{ 1, 2, 4, 5 }	[0, 999]	{4,5}		[16, 19]	FALSE, FALSE

 * 6.2.1	driving age,non-worker,17-19		DRIVING_STUDENT		{ 0, 3, 6 }		[0, 999]	{4,5}		[17, 19]	FALSE, FALSE

 * 6.2.2	driving age,non-worker,16			DRIVING_STUDENT		{ 0, 3, 6 }		[0, 999]	{0,4,5}		[16, 16]	FALSE, FALSE

 * 7.1		pre-driving age,7-15				PRE_DRIVING_STUDENT	{ 0, 3, 6 }		[0, 999]	{0,2-6}		[7, 15]		FALSE, FALSE

 * 7.2		pre-driving age,5-6					PRE_DRIVING_STUDENT	{ 0, 3, 6 }		[0, 999]	{2,3}		[5,6]		FALSE, FALSE

 * 8.1		pre-school,0-4						PRESCHOOL			{ 0, 3, 6 }		[0, 0]		{0,1-3}		[0,4]		FALSE, FALSE

 * 8.2		pre-school,5-6						PRESCHOOL			{ 0, 3, 6 }		[0, 0]		{0,1}		[5,6]		FALSE, FALSE

 * -------	----------------------------------	------------------	--------------	-----------	-----------	----------	-----------

 */
