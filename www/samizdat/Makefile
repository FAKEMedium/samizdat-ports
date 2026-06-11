PORTNAME=	samizdat
DISTVERSION=	1.0.0
CATEGORIES=	www

MAINTAINER=	hans@alipang.se
COMMENT=	Mojolicious static-content hybrid generator with a hosting panel
WWW=		https://github.com/FAKEMedium/Samizdat

LICENSE=	ART20
LICENSE_FILE=	${WRKSRC}/LICENSE

# Fetch from GitHub for now; switch to MASTER_SITES=CPAN once published as ALIPANG:
#   (remove the USE_GITHUB block, then)  MASTER_SITES=CPAN  DISTNAME=Samizdat-${DISTVERSION}
USE_GITHUB=	yes
GH_ACCOUNT=	FAKEMedium
GH_PROJECT=	Samizdat
GH_TAGNAME=	main

USES=		perl5
USE_PERL5=	configure

# Installs the rc.d scripts from files/{samizdat,minion}.in -> ${PREFIX}/etc/rc.d/
USE_RC_SUBR=	samizdat minion

NO_ARCH=	yes

# Map core's Makefile.PL PREREQ_PM to FreeBSD p5- ports. Origins below are the common
# ones; COMPLETE and VALIDATE the full list with `make` + portlint on a FreeBSD box
# (a wrong origin fails the build). `cd /usr/ports && make search name=p5-<Module>`.
RUN_DEPENDS=	p5-Mojolicious>=9.0:www/p5-Mojolicious \
		p5-Mojo-Pg>=0:databases/p5-Mojo-Pg \
		p5-Mojo-mysql>=0:databases/p5-Mojo-mysql \
		p5-Mojo-Redis>=0:databases/p5-Mojo-Redis \
		p5-Minion>=0:devel/p5-Minion \
		p5-Mojolicious-Plugin-OpenAPI>=0:www/p5-Mojolicious-Plugin-OpenAPI \
		p5-Mojolicious-Plugin-Mail>=0:mail/p5-Mojolicious-Plugin-Mail \
		p5-Mojolicious-Plugin-OAuth2>=0:www/p5-Mojolicious-Plugin-OAuth2 \
		p5-Locale-TextDomain-OO>=0:devel/p5-Locale-TextDomain-OO \
		p5-JSON-Validator>=0:devel/p5-JSON-Validator \
		p5-YAML-LibYAML>=0:textproc/p5-YAML-LibYAML \
		p5-Hash-Merge>=0:textproc/p5-Hash-Merge \
		p5-CryptX>=0:security/p5-CryptX \
		p5-Crypt-Argon2>=0:security/p5-Crypt-Argon2 \
		p5-Data-UUID>=0:devel/p5-Data-UUID \
		p5-DateTime>=0:devel/p5-DateTime \
		p5-GD-SecurityImage>=0:graphics/p5-GD-SecurityImage \
		p5-Imager>=0:graphics/p5-Imager \
		p5-Text-MultiMarkdown>=0:textproc/p5-Text-MultiMarkdown
#		... (also: Crypt-PBKDF2, Date-Calc, MIME-Lite, App-bmkpasswd,
#		Bytes-Random-Secure-Tiny, IO-Compress-Brotli, WWW-YouTube-Download, UUID)
BUILD_DEPENDS=	${RUN_DEPENDS}

.include <bsd.port.mk>
