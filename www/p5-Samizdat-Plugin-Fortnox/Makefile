PORTNAME=	Samizdat-Plugin-Fortnox
DISTVERSION=	0.01
CATEGORIES=	www perl5
PKGNAMEPREFIX=	p5-

MAINTAINER=	hans@alipang.se
COMMENT=	Fortnox accounting integration for Samizdat
WWW=		https://github.com/FAKEMedium/samizdat-fortnox

LICENSE=	ART20

# GitHub for now; switch to MASTER_SITES=CPAN (DISTNAME=Samizdat-Plugin-Fortnox-${DISTVERSION})
# once published under ALIPANG.
USE_GITHUB=	yes
GH_ACCOUNT=	FAKEMedium
GH_PROJECT=	samizdat-fortnox
GH_TAGNAME=	main

USES=		perl5
USE_PERL5=	configure
NO_ARCH=	yes

# = this dist's Makefile.PL PREREQ_PM, mapped to p5- ports (+ the core app):
RUN_DEPENDS=	samizdat>=1.0.0:www/samizdat \
		p5-Mojolicious>=9.0:www/p5-Mojolicious \
		p5-Hash-Merge>=0:textproc/p5-Hash-Merge
BUILD_DEPENDS=	${RUN_DEPENDS}

.include <bsd.port.mk>
