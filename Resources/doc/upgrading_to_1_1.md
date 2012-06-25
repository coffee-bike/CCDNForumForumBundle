set foreign_key_checks=0;


ALTER TABLE CC_Forum_Board DROP FOREIGN KEY FK_CE330F5A12469DE2;
ALTER TABLE CC_Forum_Board DROP FOREIGN KEY FK_CE330F5A2D053F64;
DROP INDEX UNIQ_CE330F5A2D053F64 ON CC_Forum_Board;
DROP INDEX IDX_CE330F5A12469DE2 ON CC_Forum_Board;
ALTER TABLE CC_Forum_Board 
	CHANGE category_id fk_category_id INT DEFAULT NULL,
	CHANGE last_post_id fk_last_post_id INT DEFAULT NULL,
	CHANGE topic_count cached_topic_count INT NOT NULL,
	CHANGE post_count cached_post_count INT NOT NULL;
ALTER TABLE CC_Forum_Board ADD CONSTRAINT FK_CE330F5A7BB031D6 FOREIGN KEY (fk_category_id) REFERENCES CC_Forum_Category(id) ON DELETE SET NULL;
ALTER TABLE CC_Forum_Board ADD CONSTRAINT FK_CE330F5AADF87F41 FOREIGN KEY (fk_last_post_id) REFERENCES CC_Forum_Post(id) ON DELETE SET NULL;
CREATE INDEX IDX_CE330F5A7BB031D6 ON CC_Forum_Board (fk_category_id);
CREATE UNIQUE INDEX UNIQ_CE330F5AADF87F41 ON CC_Forum_Board (fk_last_post_id);



ALTER TABLE CC_Forum_Draft DROP FOREIGN KEY FK_D019B289464E68B;
ALTER TABLE CC_Forum_Draft DROP FOREIGN KEY FK_D019B2891F55203D; #
ALTER TABLE CC_Forum_Draft DROP FOREIGN KEY FK_D019B2897D182D95;
ALTER TABLE CC_Forum_Draft DROP FOREIGN KEY FK_D019B289E7EC5785;
DROP INDEX IDX_D019B2897D182D95 ON CC_Forum_Draft;
DROP INDEX IDX_D019B2891F55203D ON CC_Forum_Draft; #
DROP INDEX IDX_D019B289464E68B ON CC_Forum_Draft;
DROP INDEX IDX_D019B289E7EC5785 ON CC_Forum_Draft;
ALTER TABLE CC_Forum_Draft
	 CHANGE board_id fk_board_id INT DEFAULT NULL,
	 CHANGE topic_id fk_topic_id INT DEFAULT NULL,
	 CHANGE created_by_user_id fk_created_by_user_id INT DEFAULT NULL,
	 CHANGE attachment_id fk_attachment_id INT DEFAULT NULL;
ALTER TABLE CC_Forum_Draft ADD CONSTRAINT FK_D019B289D5C4145B FOREIGN KEY (fk_board_id) REFERENCES CC_Forum_Board(id) ON DELETE SET NULL;
ALTER TABLE CC_Forum_Draft ADD CONSTRAINT FK_D019B2892D7D63E3 FOREIGN KEY (fk_topic_id) REFERENCES CC_Forum_Topic(id) ON DELETE SET NULL;
ALTER TABLE CC_Forum_Draft ADD CONSTRAINT FK_D019B289CEB06035 FOREIGN KEY (fk_created_by_user_id) REFERENCES fos_user(id) ON DELETE SET NULL;
ALTER TABLE CC_Forum_Draft ADD CONSTRAINT FK_D019B289602E9349 FOREIGN KEY (fk_attachment_id) REFERENCES CC_Component_Attachment(id) ON DELETE SET NULL;
CREATE INDEX IDX_D019B289D5C4145B ON CC_Forum_Draft (fk_board_id);
CREATE INDEX IDX_D019B2892D7D63E3 ON CC_Forum_Draft (fk_topic_id);
CREATE INDEX IDX_D019B289CEB06035 ON CC_Forum_Draft (fk_created_by_user_id);
CREATE INDEX IDX_D019B289602E9349 ON CC_Forum_Draft (fk_attachment_id);



ALTER TABLE CC_Forum_Flag DROP FOREIGN KEY FK_BD7878D0238FAC5B;
ALTER TABLE CC_Forum_Flag DROP FOREIGN KEY FK_BD7878D04B89032C;
ALTER TABLE CC_Forum_Flag DROP FOREIGN KEY FK_BD7878D069A3AAAE;
DROP INDEX IDX_BD7878D04B89032C ON CC_Forum_Flag;
DROP INDEX IDX_BD7878D0238FAC5B ON CC_Forum_Flag;
DROP INDEX IDX_BD7878D069A3AAAE ON CC_Forum_Flag;
ALTER TABLE CC_Forum_Flag 
	CHANGE post_id fk_post_id INT DEFAULT NULL, 
	CHANGE flagged_by_user_id fk_flagged_by_user_id INT DEFAULT NULL, 
	CHANGE moderated_by_user_id fk_moderated_by_user_id INT DEFAULT NULL;
ALTER TABLE CC_Forum_Flag ADD CONSTRAINT FK_BD7878D0BBA63E00 FOREIGN KEY (fk_post_id) REFERENCES CC_Forum_Post(id) ON DELETE SET NULL;
ALTER TABLE CC_Forum_Flag ADD CONSTRAINT FK_BD7878D09027E1FB FOREIGN KEY (fk_flagged_by_user_id) REFERENCES fos_user(id) ON DELETE SET NULL;
ALTER TABLE CC_Forum_Flag ADD CONSTRAINT FK_BD7878D0CFC998C2 FOREIGN KEY (fk_moderated_by_user_id) REFERENCES fos_user(id) ON DELETE SET NULL;
CREATE INDEX IDX_BD7878D0BBA63E00 ON CC_Forum_Flag (fk_post_id);
CREATE INDEX IDX_BD7878D09027E1FB ON CC_Forum_Flag (fk_flagged_by_user_id);
CREATE INDEX IDX_BD7878D0CFC998C2 ON CC_Forum_Flag (fk_moderated_by_user_id);



ALTER TABLE CC_Forum_Post DROP FOREIGN KEY FK_3606FFC71F55203D;
ALTER TABLE CC_Forum_Post DROP FOREIGN KEY FK_3606FFC7464E68B;
ALTER TABLE CC_Forum_Post DROP FOREIGN KEY FK_3606FFC77D182D95;
ALTER TABLE CC_Forum_Post DROP FOREIGN KEY FK_3606FFC78883BE77;
ALTER TABLE CC_Forum_Post DROP FOREIGN KEY FK_3606FFC7E4C7E49B;
ALTER TABLE CC_Forum_Post DROP FOREIGN KEY FK_3606FFC7FCF2A97A;
DROP INDEX IDX_3606FFC71F55203D ON CC_Forum_Post;
DROP INDEX IDX_3606FFC77D182D95 ON CC_Forum_Post;
DROP INDEX IDX_3606FFC78883BE77 ON CC_Forum_Post;
DROP INDEX IDX_3606FFC7FCF2A97A ON CC_Forum_Post;
DROP INDEX IDX_3606FFC7E4C7E49B ON CC_Forum_Post;
DROP INDEX IDX_3606FFC7464E68B ON CC_Forum_Post;
ALTER TABLE CC_Forum_Post 
	CHANGE topic_id fk_topic_id INT DEFAULT NULL, 
	CHANGE created_by_user_id fk_created_by_user_id INT DEFAULT NULL, 
	CHANGE edited_by_user_id fk_edited_by_user_id INT DEFAULT NULL, 
	CHANGE deleted_by_user_id fk_deleted_by_user_id INT DEFAULT NULL, 
	CHANGE locked_by_user_id fk_locked_by_user_id INT DEFAULT NULL, 
	CHANGE attachment_id fk_attachment_id INT DEFAULT NULL;
ALTER TABLE CC_Forum_Post ADD CONSTRAINT FK_3606FFC72D7D63E3 FOREIGN KEY (fk_topic_id) REFERENCES CC_Forum_Topic(id) ON DELETE SET NULL;
ALTER TABLE CC_Forum_Post ADD CONSTRAINT FK_3606FFC7CEB06035 FOREIGN KEY (fk_created_by_user_id) REFERENCES fos_user(id) ON DELETE SET NULL;
ALTER TABLE CC_Forum_Post ADD CONSTRAINT FK_3606FFC746B4308F FOREIGN KEY (fk_edited_by_user_id) REFERENCES fos_user(id) ON DELETE SET NULL;
ALTER TABLE CC_Forum_Post ADD CONSTRAINT FK_3606FFC74F5AE4DA FOREIGN KEY (fk_deleted_by_user_id) REFERENCES fos_user(id) ON DELETE SET NULL;
ALTER TABLE CC_Forum_Post ADD CONSTRAINT FK_3606FFC72AF06A63 FOREIGN KEY (fk_locked_by_user_id) REFERENCES fos_user(id) ON DELETE SET NULL;
ALTER TABLE CC_Forum_Post ADD CONSTRAINT FK_3606FFC7602E9349 FOREIGN KEY (fk_attachment_id) REFERENCES CC_Component_Attachment(id) ON DELETE SET NULL;
CREATE INDEX IDX_3606FFC72D7D63E3 ON CC_Forum_Post (fk_topic_id);
CREATE INDEX IDX_3606FFC7CEB06035 ON CC_Forum_Post (fk_created_by_user_id);
CREATE INDEX IDX_3606FFC746B4308F ON CC_Forum_Post (fk_edited_by_user_id);
CREATE INDEX IDX_3606FFC74F5AE4DA ON CC_Forum_Post (fk_deleted_by_user_id);
CREATE INDEX IDX_3606FFC72AF06A63 ON CC_Forum_Post (fk_locked_by_user_id);
CREATE INDEX IDX_3606FFC7602E9349 ON CC_Forum_Post (fk_attachment_id);



ALTER TABLE CC_Forum_Registry DROP FOREIGN KEY FK_156659CE6DD3F56D;
DROP INDEX IDX_156659CE6DD3F56D ON CC_Forum_Registry;
ALTER TABLE CC_Forum_Registry 
	CHANGE cachePostCount cached_post_count INT NOT NULL, 
	CHANGE cacheKarmaPositiveCount cached_karma_positive_count INT NOT NULL, 
	CHANGE cacheKarmaNegativeCount cached_karma_negative_count INT NOT NULL, 
	CHANGE owned_by_user_id fk_owned_by_user_id INT DEFAULT NULL;
ALTER TABLE CC_Forum_Registry ADD CONSTRAINT FK_156659CE3BB9921A FOREIGN KEY (fk_owned_by_user_id) REFERENCES fos_user(id) ON DELETE SET NULL;
CREATE INDEX IDX_156659CE3BB9921A ON CC_Forum_Registry (fk_owned_by_user_id);



ALTER TABLE CC_Forum_Subscription DROP FOREIGN KEY FK_F00B98B81F55203D;
ALTER TABLE CC_Forum_Subscription DROP FOREIGN KEY FK_F00B98B86DD3F56D;
DROP INDEX IDX_F00B98B81F55203D ON CC_Forum_Subscription;
DROP INDEX IDX_F00B98B86DD3F56D ON CC_Forum_Subscription;
ALTER TABLE CC_Forum_Subscription 
	CHANGE topic_id fk_topic_id INT DEFAULT NULL, 
	CHANGE owned_by_user_id fk_owned_by_user_id INT DEFAULT NULL, 
	CHANGE read_it is_read TINYINT(1) NOT NULL, 
	CHANGE subscribed is_subscribed TINYINT(1) NOT NULL;
ALTER TABLE CC_Forum_Subscription ADD CONSTRAINT FK_F00B98B82D7D63E3 FOREIGN KEY (fk_topic_id) REFERENCES CC_Forum_Topic(id) ON DELETE SET NULL;
ALTER TABLE CC_Forum_Subscription ADD CONSTRAINT FK_F00B98B83BB9921A FOREIGN KEY (fk_owned_by_user_id) REFERENCES fos_user(id) ON DELETE SET NULL;
CREATE INDEX IDX_F00B98B82D7D63E3 ON CC_Forum_Subscription (fk_topic_id);
CREATE INDEX IDX_F00B98B83BB9921A ON CC_Forum_Subscription (fk_owned_by_user_id);



ALTER TABLE CC_Forum_Topic DROP FOREIGN KEY FK_B25FA061B93E802;
ALTER TABLE CC_Forum_Topic DROP FOREIGN KEY FK_B25FA062D053F64;
ALTER TABLE CC_Forum_Topic DROP FOREIGN KEY FK_B25FA0658056FD0;
ALTER TABLE CC_Forum_Topic DROP FOREIGN KEY FK_B25FA06E7EC5785;
ALTER TABLE CC_Forum_Topic DROP FOREIGN KEY FK_B25FA06FCF2A97A;
DROP INDEX UNIQ_B25FA0658056FD0 ON CC_Forum_Topic;
DROP INDEX UNIQ_B25FA062D053F64 ON CC_Forum_Topic;
DROP INDEX IDX_B25FA06E7EC5785 ON CC_Forum_Topic;
DROP INDEX IDX_B25FA061B93E802 ON CC_Forum_Topic;
DROP INDEX IDX_B25FA06FCF2A97A ON CC_Forum_Topic;
ALTER TABLE CC_Forum_Topic 
	CHANGE board_id fk_board_id INT DEFAULT NULL, 
	CHANGE first_post_id fk_first_post_id INT DEFAULT NULL, 
	CHANGE last_post_id fk_last_post_id INT DEFAULT NULL, 
	CHANGE closed_by_user_id fk_closed_by_user_id INT DEFAULT NULL, 
	CHANGE deleted_by_user_id fk_deleted_by_user_id INT DEFAULT NULL, 
	CHANGE view_count cached_view_count INT NOT NULL, 
	CHANGE reply_count cached_reply_count INT NOT NULL;
ALTER TABLE CC_Forum_Topic ADD CONSTRAINT FK_B25FA06D5C4145B FOREIGN KEY (fk_board_id) REFERENCES CC_Forum_Board(id) ON DELETE SET NULL;
ALTER TABLE CC_Forum_Topic ADD CONSTRAINT FK_B25FA063C4F1A12 FOREIGN KEY (fk_first_post_id) REFERENCES CC_Forum_Post(id) ON DELETE SET NULL;
ALTER TABLE CC_Forum_Topic ADD CONSTRAINT FK_B25FA06CD83D7D FOREIGN KEY (fk_last_post_id) REFERENCES CC_Forum_Post(id) ON DELETE SET NULL;
ALTER TABLE CC_Forum_Topic ADD CONSTRAINT FK_B25FA06D5A466FA FOREIGN KEY (fk_closed_by_user_id) REFERENCES fos_user(id) ON DELETE SET NULL;
ALTER TABLE CC_Forum_Topic ADD CONSTRAINT FK_B25FA064F5AE4DA FOREIGN KEY (fk_deleted_by_user_id) REFERENCES fos_user(id) ON DELETE SET NULL;
CREATE INDEX IDX_B25FA06D5C4145B ON CC_Forum_Topic (fk_board_id);
CREATE UNIQUE INDEX UNIQ_B25FA063C4F1A12 ON CC_Forum_Topic (fk_first_post_id);
CREATE UNIQUE INDEX UNIQ_B25FA06CD83D7D ON CC_Forum_Topic (fk_last_post_id);
CREATE INDEX IDX_B25FA06D5A466FA ON CC_Forum_Topic (fk_closed_by_user_id);
CREATE INDEX IDX_B25FA064F5AE4DA ON CC_Forum_Topic (fk_deleted_by_user_id);

set foreign_key_checks=1;